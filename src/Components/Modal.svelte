<!-- ModalForm.svelte -->
<script>
    import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  let values = {
    taskName: '',
    taskDetails: '',
    assignedTo:'',
    dateTime:'',
    priorityLevel:'',
  };


  function handleSubmit() {
    const formValues = { ...values };
    dispatch('submit', formValues); // Emitting the submit event with form values
    values = {  taskName: '',
    taskDetails: '',
    assignedTo:'',
    dateTime:'',
    priorityLevel:''  }; // Resetting form values
  }
  
</script>

<div class="modal-form">
  <form on:submit|preventDefault={handleSubmit}>
    <h3>New Task</h3>
    <label for="taskName">Task Name</label><br>
    <input type="text" name="taskName" bind:value={values.taskName}><br>

     <label for="taskDetails">Task Details</label><br>
    <input type="text" name="taskDetails" bind:value={values.taskDetails}><br>

     <label for="assignedTo">Assigned To</label><br>
    <input type="text" name="assignedTo" bind:value={values.assignedTo}><br>

     <label for="dateTime">Date Time</label>
    <input type="datetime-local" name="dateTime" bind:value={values.dateTime}><br><br>
    
    <label for="priorityLevel">Priority Level:</label>

    <label for="High">
      <input type="radio" name="priorityLevel" value="High" bind:group={values.priorityLevel}>
      High
    </label>

    <label for="Medium">
      <input type="radio" name="priorityLevel" value="Medium" bind:group={values.priorityLevel}>
      Medium
    </label>

    <label for="Low">
      <input type="radio" name="priorityLevel" value="Low" bind:group={values.priorityLevel}>
      Low
    </label><br><br>

   

    

    <button type="submit">Submit</button><br>
  </form>
</div>

<!-- ModalForm.svelte -->
<style>
  .modal-form {
    padding: 20px;
    background-color:  #f2f2f2;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    font-family: Arial, sans-serif;
  }

  .modal-form h3 {
    margin-top: 0;
    font-size: 24px;
    color: #0a0a0a;
  }

  .modal-form label {
    display: inline-block;
    margin-bottom: 5px;
    font-weight: bold;
    color: #0a0a0a;
  }

  .modal-form input[type="text"],
  .modal-form input[type="datetime-local"],
  .modal-form input[type="number"] {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 16px;
    box-sizing: border-box;
  }

  .modal-form input[type="radio"] {
    margin-right: 10px;
    display: flex;
    justify-content:space-around;
  }

  .modal-form button[type="submit"] {
    display: block;
    width: 100%;
    padding: 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
  }

  .modal-form button[type="submit"]:hover {
    background-color: #0056b3;
  }

  /* Additional CSS for radio buttons in a single line */
  .modal-form label input[type="radio"] {
    display: inline-block;
    vertical-align: baseline;
  }
</style>
