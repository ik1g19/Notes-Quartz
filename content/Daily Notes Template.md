# <mark style="background: #ABF7F7A6;">Focus</mark> => <mark style="background: #BBFABBA6;">Here</mark> 

# <mark style="background: #ABF7F7A6;">Notes</mark>



# <mark style="background: #ABF7F7A6;">To Do</mark>

![[!/To Do|To Do]]
# <mark style="background: #ABF7F7A6;">Job Applications</mark>

- [ ] 1/5 Jobs
	- [ ] 2/5 Jobs
	- [ ] 3/5 Jobs
	- [ ] 4/5 Jobs
	- [ ] 5/5 Jobs
# <mark style="background: #ABF7F7A6;">Habits</mark>

- [ ] `$= dv.page("Habits").habit_music_theory`
- [ ] `$= dv.page("Habits").habit_leetcode`
- [ ] `$= dv.page("Habits").habit_dev_django`
- [ ] `$= dv.page("Habits").habit_dev_spring` 
- [ ] `$= dv.page("Habits").habit_study_plan` 

#daily-note

```dataviewjs
// DataviewJS snippet for task progress bar

// Get all tasks from the current file
let currentFile = dv.current();

// Filter tasks that contain the word "jobs"
let allTasks = currentFile.file.tasks.filter(t => t.text.toLowerCase().includes('habit'));

// Count completed tasks and total tasks
let completedTasks = allTasks.filter(t => t.completed).length;
let totalTasks = allTasks.length;

// Avoid division by zero
let progress = totalTasks === 0 ? 0 : Math.floor((completedTasks / totalTasks) * 100);

// Set progress bar color to #4caf50 when progress is 100%, otherwise keep the original color
let progressBarColor = progress === 100 ? '#4caf50' : '#2b8089';

// Render progress bar
let progressBar = ` <div style="text-align: center; margin-top: 10px;"> 
<div style="background-color: #ddd; border-radius: 10px; padding: 2px; width: 80%; display: inline-block;"> 
<div style="background-color:${progressBarColor}; width: ${progress}%; height: 4px; border-radius: 10px;"></div> </div> </div>`;

dv.paragraph(`${completedTasks}/${totalTasks} Habits Completed`);
dv.paragraph(progressBar);

```

```dataviewjs
// DataviewJS snippet for task pr ogress bar

// Get all tasks from the current file
let currentFile = dv.current();

// Filter tasks that contain the word "jobs"
let allTasks = currentFile.file.tasks.filter(t => t.text.toLowerCase().includes('jobs'));

// Count completed tasks and total tasks
let completedTasks = allTasks.filter(t => t.completed).length;
let totalTasks = allTasks.length;

// Avoid division by zero
let progress = totalTasks === 0 ? 0 : Math.floor((completedTasks / totalTasks) * 100);

// If progress is greater than 100, set it to 100 
if (progress > 100) { 
progress = 100; 
}

// Set progress bar color to #4caf50 when progress is 100%, otherwise keep the original color
let progressBarColor = progress === 100 ? '#4caf50' : '#a9415e';

// Render progress bar
let progressBar = ` <div style="text-align: center; margin-top: 10px;"> 
<div style="background-color: #ddd; border-radius: 10px; padding: 2px; width: 80%; display: inline-block;"> 
<div style="background-color: ${progressBarColor}; width: ${progress}%; height: 4px; border-radius: 10px;"></div> </div> </div>`;

dv.paragraph(`${completedTasks}/${totalTasks} Job Applications`);
dv.paragraph(progressBar);

```
