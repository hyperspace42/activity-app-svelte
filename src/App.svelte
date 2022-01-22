<script>
  import Chance from 'chance';
  import getActivityFromApi from './api';

  const chance = Chance();

  const gradients = ['blue_gradient', 'purple_gradient', 'yellow_gradient', 'green_gradient']
  let randomGradientNumber = 0

  let activity;
  let type;
  let price;
  let participants;

  async function getActivity() {
    const res = await getActivityFromApi();
    randomGradientNumber = chance.integer({ min: 0, max: 3 });

    activity = res.activity;
    type = res.type;
    price = res.price;
    participants = res.participants;
  }
</script>

<div class="container">
  <div class="screen">
    <p class="screen_title">Have nothing to do?</p>
    <button on:click={getActivity} class="screen_button">Click on me</button>
  </div>
  <div class="screen_res">
    {#if type}
      <div class="screen_res_type">
        <p class="screen_text {gradients[randomGradientNumber]}">{type}</p>
      </div>
    {/if}
    {#if activity}
    <div class="screen_res_block">
      <p class="screen_text">{activity}</p>
    </div>
    {/if}
    {#if price}
    <div class="screen_res_type">
      <p class="screen_text">Price: {price}<span class="{gradients[randomGradientNumber]}">$</span></p>
    </div>
    {/if}
    {#if participants}
    <div class="screen_res_block">
      <p class="screen_text">Participants: {participants}</p>
    </div>
    {/if}
  </div>
</div>

<style>
  .container {
    padding: 0 2rem;
    margin: 0 auto;
  }

  .screen {
    text-align: center;
  }

  .screen_title {
    font-size: 2rem;
    color: #e6e6e6;
  }

  .screen_button {
    font-size: 1.5rem;
    color: #e6e6e6;
    background: #111111;
    padding: 0.7rem 1rem;
    border: 2px solid #1d1d1d;
    border-radius: 1.2rem;
    transition: all ease 0.1s;
  }

  .screen_button:hover {
    background: #1d1d1d;
  }

  .screen_text {
    font-size: 1.5rem;
    color: #e6e6e6;
    margin: .25rem 0;
  }

  .screen_text:first {
    margin: .75rem 0;
  }

  .screen_res {
    text-align: center;
    margin-top: 1rem;
  }

  .screen_res_type {
    width: auto;
    display: inline-block;
  }

</style>
