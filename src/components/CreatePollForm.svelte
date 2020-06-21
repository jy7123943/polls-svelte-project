<script>
  import PollStore from '../stores/PollStore.js';
  import Button from '../shared/Button.svelte';
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let fields = { question: '', answerA: '', answerB: '', };
  let errors = { question: '', answerA: '', answerB: '', };

  let isValid = false;

  const handleSubmit = () => {
    isValid = true;
    // validate question
    if (fields.question.trim().length < 5) {
      isValid = false;
      errors.question = 'Question must be at lease 5 characters long';
    } else {
      errors.question = '';
    }

    // validate answer A
    if (fields.answerA.trim().length < 1) {
      isValid = false;
      errors.answerA = 'Answer A cannot be empty';
    } else {
      errors.answerA = '';
    }

    // validate answer B
    if (fields.answerB.trim().length < 1) {
      isValid = false;
      errors.answerB = 'Answer B cannot be empty';
    } else {
      errors.answerB = '';
    }

    if (isValid) {
      let poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
      // save poll to store
      PollStore.update(currentPolls => {
        return [poll, ...currentPolls]
      });
      dispatch('add');
      fields.question = '';
      fields.answerA = '';
      fields.answerB = '';
    }
  };
</script>

<form on:submit|preventDefault={handleSubmit}>
  <div class='form-field'>
    <label for='question'>Poll Question:</label>
    <input type='text' id='question' bind:value={fields.question} />
    <div class='error'>{errors.question}</div>
  </div>
  <div class='form-field'>
    <label for='answerA'>Answer A:</label>
    <input type='text' id='answerA' bind:value={fields.answerA} />
    <div class='error'>{errors.answerA}</div>
  </div>
  <div class='form-field'>
    <label for='answerB'>Answer B:</label>
    <input type='text' id='answerB' bind:value={fields.answerB} />
    <div class='error'>{errors.answerB}</div>
  </div>
  <Button type='secondary' flat={true}>Add Poll</Button>
</form>

<style>
  form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
  }
  .form-field {
    margin: 18px auto;
  }
  input {
    width: 100%;
    border-radius: 6px;
  }
  label {
    margin: 10px auto;
    text-align: left;
  }
  .error {
    font-weight: bold;
    font-size: 12px;
    color: #d91b42;
  }
</style>
