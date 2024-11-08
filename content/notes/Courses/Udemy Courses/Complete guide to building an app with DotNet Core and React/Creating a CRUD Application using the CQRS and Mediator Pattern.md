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

[[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Walking Skeleton Part 1 - Dotnet#^create-act-controller|Original Version for Comparison]]

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

