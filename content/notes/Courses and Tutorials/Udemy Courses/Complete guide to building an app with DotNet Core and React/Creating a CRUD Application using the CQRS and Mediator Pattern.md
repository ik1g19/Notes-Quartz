# Clean Architecture

![[Images/camera_capture 1.jpg]]

![[Images/camera_capture 2.jpg]]

![[Images/camera_capture 3.jpg]]
# CQRS

>[!INFO]
>Command Query Responsibility Segregation


| Command                   | Query                   |
| ------------------------- | ----------------------- |
| Does something            | Answers a Quetion       |
| Modifies State            | Should not Modify State |
| Should not Return a Value | Returns a Value         |

![[Images/camera_capture 4.jpg]]

![[Images/camera_capture 5.jpg]]

# Creating our First Query Handler

Add MediatR to the `Application` project with NuGet

We create a class that will hold a list of our Activities

📁`Application\Activities\List.cs`
```cs
using Domain;
using MediatR;
using Microsoft.EntityFrameworkCore;
using Persistence;

namespace Application.Activities
{
    public class List
    {
        public class Query : IRequest<List<Activity>> {}

        public class Handler : IRequestHandler<Query, List<Activity>>
        {
            private readonly DataContext _context;

            public Handler(DataContext context) {
                _context = context;
            }

            public async Task<List<Activity>> Handle(Query request, CancellationToken cancellationToken)
            {
                return await _context.Activities.ToListAsync();
            }
        }
    }
}
```

We now go back to the Activities Controller and utilize MediatR

[[notes/Courses and Tutorials/Udemy Courses/Complete guide to building an app with DotNet Core and React/Walking Skeleton Part 1 - Dotnet#^create-act-controller|Original Version for Comparison]]

📁`API\Controllers\ActivitiesController.cs`
```cs
using Application.Activities;
using Domain;
using MediatR;
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    public class ActivitiesController : BaseApiController
    {
        private readonly IMediator _mediator;

        public ActivitiesController(IMediator mediator)
        {
            _mediator = mediator;
        }

        [HttpGet]
        public async Task<ActionResult<List<Activity>>> GetActivities()
        {
            return await _mediator.Send(new List.Query());
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<Activity>> GetActivity(Guid id)
        {
            return Ok();
        }
    }
}
```

We now need to register MediatR as a service

📁`API\Program.cs`
```cs
...
// Add services to the container.

builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
builder.Services.AddDbContext<DataContext>(opt => {
    opt.UseSqlite(builder.Configuration.GetConnectionString("DefaultConnection"));
});
builder.Services.AddCors(opt => {
    opt.AddPolicy("CorsPolicy", policy => {
        policy.AllowAnyHeader().AllowAnyMethod().WithOrigins("http://localhost:3000");
    });
});
builder.Services.AddMediatR(cfg => cfg.RegisterServicesFromAssembly(typeof(List.Handler).Assembly));
...
```

Now our GET requests do not come from the API controller directly, but rather through MediatR

# Thin Controllers in the API

To thin our `ActivitiesController` we move MediatR to the `BaseApiController`

📁`API\Controllers\ActivitiesController.cs`
```cs
using Application.Activities;
using Domain;
using MediatR;
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    public class ActivitiesController : BaseApiController
    {

        [HttpGet]
        public async Task<ActionResult<List<Activity>>> GetActivities()
        {
            return await Mediator.Send(new List.Query());
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<Activity>> GetActivity(Guid id)
        {
            return Ok();
        }
    }
}
```

📁`API\Controllers\BaseApiController.cs`
```cs
using MediatR;
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class BaseApiController : ControllerBase
    {
        private IMediator _mediator;

        //populate variable with mediatr service
        protected IMediator Mediator => _mediator ??= 
            HttpContext.RequestServices.GetService<IMediator>();
    }
}
```

# Adding a Details Handler

We are now going to create a new Handler for returning an individual Activities details

We start with creating a `Details` class

📁`Application\Activities\Details.cs`
```cs
using Domain;
using MediatR;
using Persistence;

namespace Application.Activities
{
    public class Details
    {
        public class Query : IRequest<Activity> {
            public Guid Id { get; set; }
        }

        public class Handler : IRequestHandler<Query, Activity>
        {
            private readonly DataContext _context;
            public Handler(DataContext context)
            {
                _context = context;
            }

            public async Task<Activity> Handle(Query request, CancellationToken cancellationToken)
            {
                return await _context.Activities.FindAsync(request.Id);
            }
        }
    }
}
```

We can now use this in `ActivitiesController`

📁`API\Controllers\ActivitiesController.cs`
```cs
using Application.Activities;
using Domain;
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    public class ActivitiesController : BaseApiController
    {

        [HttpGet]
        public async Task<ActionResult<List<Activity>>> GetActivities()
        {
            return await Mediator.Send(new List.Query());
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<Activity>> GetActivity(Guid id)
        {
            return await Mediator.Send(new Details.Query{Id = id});
        }
    }
}
```

# Adding a Create Handler

Create a `create` class

📁`Application\Activities\Create.cs`
```cs
using Domain;
using MediatR;
using Persistence;

namespace Application.Activities
{
    public class Create
    {
        public class Command : IRequest {
            // what we want to receive as a parameter from the API
            public Activity Activity {get; set;}
        }

        public class Handler : IRequestHandler<Command>
        {
            private readonly DataContext _context;

            public Handler(DataContext context)
            {
            _context = context;
            }

            public async Task Handle(Command request, CancellationToken cancellationToken)
            {
                _context.Activities.Add(request.Activity);

                await _context.SaveChangesAsync();
            }
        }
    }
}
```

We now create the endpoint in the `ActivitiesController`

📁`API\Controllers\ActivitiesController.cs`
```cs
using Application.Activities;
using Domain;
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    public class ActivitiesController : BaseApiController
    {

        [HttpGet]
        public async Task<ActionResult<List<Activity>>> GetActivities()
        {
            return await Mediator.Send(new List.Query());
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<Activity>> GetActivity(Guid id)
        {
            return await Mediator.Send(new Details.Query{Id = id});
        }

        // Endpoint for creating an activity
        [HttpPost]
        public async Task<IActionResult> CreateActivity(Activity activity) {
            await Mediator.Send(new Create.Command {Activity = activity});

            return Ok();
        }
    }
}
```

# Adding an Edit Handler

Create an `Edit` class

📁`Application\Activities\Edit.cs`
```cs
using Domain;
using MediatR;
using Persistence;

namespace Application.Activities
{
    public class Edit
    {
        public class Command : IRequest {
            public Activity Activity {get; set;}
        }

        public class Handler : IRequestHandler<Command> {
            public DataContext _context { get; }

            public Handler(DataContext context) {
            _context = context;

            }

            public async Task Handle(Command request, CancellationToken cancellationToken)
            {
                var activity = await _context.Activities.FindAsync(request.Activity.Id);

                activity.Title = request.Activity.Title ?? activity.Title;

                await _context.SaveChangesAsync();
            }
        }
    }
}
```

Create the `Put` endpoint in the `ActivitiesController`

This time the endpoint accepts a parameter

📁`API\Controllers\ActivitiesController.cs`
```cs
...
// Endpoint for editing an activity
[HttpPut("{id}")]
public async Task<IActionResult> EditActivity(Guid id, Activity activity) {
	activity.Id = id;

	await Mediator.Send(new Edit.Command {Activity = activity});

	return Ok();
}
...
```

# Adding `AutoMapper`

We create a new `Core` folder in our application project

`Core` will be responsible for things that are applicable to all of our features

We use `NuGet` gallery to add the `AutoMapper` `DependencyInjection` to our `Application` project

We create a `MappingProfiles` class

📁`Application\Core\MappingProfiles.cs`
```cs
using AutoMapper;
using Domain;

namespace Application.Core
{
    public class MappingProfiles : Profile
    {
        public MappingProfiles() {
            CreateMap<Activity, Activity>();
        }
    }
}
```

Now, instead of `activity.Title = request.Activity.Title ?? activity.Title;`

We can use `AutoMapper`

📁`Application\Activities\Edit.cs`
```cs
...
public class Handler : IRequestHandler<Command> {
	public DataContext _context { get; }
	private readonly IMapper _mapper;

	public Handler(DataContext context, IMapper mapper) {
		_mapper = mapper;
		_context = context;
	}

	public async Task Handle(Command request, CancellationToken cancellationToken)
	{
		var activity = await _context.Activities.FindAsync(request.Activity.Id);

		_mapper.Map(request.Activity, activity);

		await _context.SaveChangesAsync();
	}
}
...
```

This now means we can allow a user to update all of a fields properties at once

Since we have now added a new dependency we add it to the `Services` section of `Program`

📁`API\Program.cs`
```cs
...
builder.Services.AddAutoMapper(typeof(MappingProfiles).Assembly);
...
```

# Adding a Delete Handler

