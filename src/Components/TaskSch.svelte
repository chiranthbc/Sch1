<script>
// @ts-nocheck

  import ModalForm from './Modal.svelte';
	import ModalSch from './ModalSch.svelte';

  let formModal = false;
  
  let tasks = [];
  
  let editIndex = null; // Track the index of the task being edited
  


  function handleFormSubmit(event) {
     const { schName,
    resourceName,
    frequency,
    runEvery,
    time,
    failureAttempts,
    status,
  } = event.detail;
     
      

   const updatedTask = {
    schName,
    resourceName,
    frequency,
    runEvery,
    time,
    failureAttempts,
    status,
  };

   
    if (editIndex !== null) {
      // If editIndex is not null, update existing task
     
      tasks[editIndex] = updatedTask;
      editIndex = null; // Reset editIndex after editing
     
      console.log("Task Edited:", tasks);
    } else {
      // If editIndex is null, add a new task
      
      tasks = [...tasks, updatedTask];
      console.log("New Task Added:", tasks);
    }
    formModal = false; // Close the modal after submission
  }

  
  function deleteTask(index) {
  
    tasks = tasks.filter((_, i) => i !== index);
    console.log("Task deleted:", tasks);
  }

 
  function editTask(index) {
    // Set the editIndex and populate form with existing task details
   
    editIndex = index;
    
    const taskToEdit = tasks[index];
    // Open modal for editing
    formModal = true;
    // Update form values with task details for editing
    
    values = {
    schName: taskToEdit.schName,
    resourceName: taskToEdit.resourceName,
    frequency: taskToEdit.frequency,
    runEvery: taskToEdit.runEvery,
    time: taskToEdit.time,
    failureAttempts: taskToEdit.failureAttempts,
    status: taskToEdit.status,

  };
  }
  

  
  
  function handleRunTask() {
    console.log("Tasks:", tasks); // Log the tasks array
  
  }
</script>


<div class="task-manager">
    <div class="header">
      <h1> SCHEDULES</h1>
      <div class="header-buttons">
          <button on:click={() => (formModal = true)} class="add-task-button">Create Schedule</button>
         
      </div>
      <div class="modal">
        {#if formModal}
          <ModalSch on:submit={handleFormSubmit} />
        {/if}
      </div>
    </div>

     {#if !formModal}
    <div class="task-manager-header">
          <h2>Schedule Name</h2>
          <h2>Resource Name</h2>
          <h2>Frequency</h2>
          <!-- <h2>Time</h2> -->
          <h2>Status</h2>
          <h2>Edit</h2>
         
      </div>
      <div class="task-manager-list">
            <!-- Displaying Tasks -->
            {#each tasks as task, index (task)}
             <!-- Use a unique variable for each task's selection -->
             
                <div class="task-manager-list-item" key={task.task}>
                  <h2>{task.schName}</h2>
                  <h2>{task.resourceName}</h2>
                  <h2>{task.frequency}</h2>
                  <!-- <h2>{task.time}</h2> -->
                  <h2>{task.status}</h2>
                  <div class="edit">
                    <button on:click={() => deleteTask(index)} class="delete-task-button"><i class="fa-solid fa-trash-can"></i></button>
                    <button on:click={() => editTask(index)} class="edit-task-button"><i class="fa-solid fa-pen-to-square"></i></button>
                  </div>

                 
                </div>
                
            {/each}
        </div>
    {/if}     
</div>


 
<style>
  .task-manager {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    overflow: hidden;
    
  }

  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
    margin-right: 20px;
    margin-left: 20px;
  }

  .header h1 {
    font-weight: bold;
    font-size: 24px;
    display: flex;
    align-items: center;
  }

  .header h1 i {
    margin-right: 5px;
  }
.header-buttons {
  display: flex;
  gap: 10px;
}
.header-buttons button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background-color: #3498db;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.header-buttons button:hover {
  background-color: #2980b9;
}


  .task-manager-header {
      display: grid; /* Use grid for more precise control */
  grid-template-columns: repeat(5, 1fr); /* Create 4 equally spaced columns */
  background-color: rgb(190, 196, 203);
  margin-left: 10px;
  margin-right: 10px;
  padding: 8px; /* Add padding for spacing */
  font-weight: bold;
  font-size: 16px;
  gap: 10px;
  }

  

  .task-manager-list-item {
  display: grid; 
  grid-template-columns: repeat(5, 1fr); 
  align-items: center;
  padding: 8px;
  font-weight: normal;
  border-bottom: 1px solid #ccc;
  font-size: 14px;
   gap: 10px;

  }

 .delete-task-button {
    background-color: #ff6347;
  color: white;
  border: none;
 
  border-radius: 4px;
  cursor: pointer;
  width: fit-content;
  transition: background-color 0.3s ease; 
  padding: 10px;
  margin-right: 5px;
  
} 
.edit-task-button {
    background-color: #ff6347;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    padding: 10px;
    
    transition: background-color 0.3s ease;  /* Smooth transition on hover */
}
.edit {
    position: relative;
    display: inline-block;
  }

 

  .delete-task-button:hover {
    background-color: #ff7f50;
  } 
  .edit-task-button:hover {
    background-color: #ff7f50;
  } 

  .modal {
    position: fixed;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 30%;
    height: 40%;
    z-index: 9999;
    
  }
/* overflow: auto; 
    z-index: 9999; */
/* .job-dropdown {
    
    position: relative;
    display: inline-block;
  } */

 
.run-task {
    display: flex;
    justify-content:flex-start;
    align-items: flex-start;
  }
  .run-task button {
    /* Adjust button styles as needed */
    background-color: #008CBA;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    padding: 8px 16px;
    transition: background-color 0.3s ease; /* Smooth transition on hover */
  }

  .run-task button:hover {
    background-color: #005f73;
  }

  

  /* Additional styles as needed */
</style>