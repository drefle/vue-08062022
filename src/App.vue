<template>

  <div class="page">

    <div class="card">

      <div class="balance">

      <div class="balance__wrapper">
        <h3>My balance</h3>
        <h2>$921.48</h2>
      </div>
      <svg class="logo" width="72" height="48" viewBox="0 0 72 48" xmlns="http://www.w3.org/2000/svg"><g fill="none" fill-rule="evenodd"><circle fill="#382314" cx="48" cy="24" r="24"/><circle stroke="#FFF" stroke-width="2" cx="24" cy="24" r="23"/></g></svg>
      
      </div>

      <div class="chart__wrapper">

          <h2 class="spending">Spending - Last 7 days</h2>
          <div class="days">
            <Day v-for="day in days" :key="day.name" :name="day.day" :amount="day.amount"/>
          </div>

          <div class="footer">

            <div class="thisMonth">
              <p>Total this month</p>
              <h1>$478.33</h1>
            </div>

            <div class="lastMonth">
              <h3>+2.4%</h3>
              <p>from last month</p>
            </div>

          </div>
          
      </div>

    </div>
    
  </div>
  

</template>

<script>
import Day from '@/components/Day.vue';
  export default {
    components: {
      Day,
    },
    data() {
      return {
        days: []
      }
    },
    async beforeMount() {
      const response = await fetch('../data.json');
      const days = await response.json();
      this.days = days;
    },
  }
</script>

<style lang="scss">

body{
  	margin: 0;
	padding: 0;
	border: 0;
}

.page{
  height: 100vh;
  width: 100%;
  background-color: hsl(27,66%,92%);
  display: flex;
  justify-content: center;
  align-items: center;
}
.card{
    padding: 0 2rem;
    width: clamp(375px,100%,475px);
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    gap: 1rem;
}
.balance {
    display: flex;
    justify-content: space-between;
    background-color: hsl(10,79%,65%);
    border-radius: 0.5rem;
    padding: 1rem;
    color: white;
    font-family: 'DM Sans';
    .balance__wrapper{
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
      h3 {
          font-weight: 100;
          font-size: 12px;
      }
      h2 {
          font-weight: 700;
          font-size: 18px;
          letter-spacing: 1px;
      }
    }
}

.chart__wrapper {
    background-color: hsl(33,100%,98%);
    padding: 2rem;
    font-family: "DM Sans";
    display: flex;
    flex-direction: column;
    gap: 2rem;
    border-radius: 0.5rem;

    .spending{
      color: hsl(25,47%,15%);
      font-size: 24px;
      font-weight: 700;
    }

    .days{
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: .5rem;
      align-items: end;
      padding-top:1rem ;
    }

    .days :nth-child(3) .colonne{
      background-color: hsl(186, 34%, 60%);
    }

    .footer{
      border-top: 2px solid hsl(27,66%,92%);
      padding-top: 1.5rem;
      display: flex;
      justify-content: space-between;

      .thisMonth {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;

        h1 {
          font-size: clamp(24px,7vw,35px);
          font-weight: 700;
          color: hsl(25,47%,15%);
        }
      }

      .lastMonth {
        display: flex;
        flex-direction: column;
        gap: 0.2rem;
        align-items: end;
        box-sizing: content-box;
        padding-top: 2.2rem;

        h3{
          font-size: 14px;
          font-weight: 700;
          color: hsl(25,47%,15%);
        }

      }
      p {
          font-size: clamp(10px,2vw,14px);
          color: hsl(28,10%,53%);
        }
    }
}

</style>