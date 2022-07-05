<template>
<div class="container">
  <div class="total-balance-container">
    <div class="total-balance-info">
        <p class="total-balance-title">My balance</p>
        <p class="total-balance-funds">${{availableFunds}}</p>
    </div>
    <div class="total-balance-icon">
        <img src="../assets/logo.svg" alt="logo">
    </div>
  </div>
  <div class="chart-container">
    <h3>Spending - Last 7 days</h3>

    <ul class="data-container">
        <li v-for="info in dataFromBackend" :key="info.day" class="day-name">
        <span v-if="info.isVisible" class="tooltip">${{ info.amount }}</span>
        <div
        class="chart-bar"
        :class="isCurrentDay === info.day ? 'today' : ''"
        :style="{'height': info.amount * 3 +'px'}"
        @mouseover.self="showTooltip(info.day)"
        @mouseleave.self="showTooltip(info.day)"></div>
            {{ info.day }}
        </li>
    </ul>

    <hr>
    <div class="total-expenses-container">
        <div class="total-expenses-amount">
            <p class="expenses-text">Total this month</p>
            <p class="expenses-total">${{totalExpenses}}</p>
        </div>
        <div class="total-expenses-details">
            <p class="expenses-diff">+2.4%</p>
            <p class="expenses-text">from last month</p>
        </div>
    </div>
  </div>
</div>
</template>

<script>
import data from '../helpers/data.json';
import { reactive, computed } from 'vue';

export default {
    
    setup() {
        const availableFunds = 921.48;
        const totalExpenses = 478.33;


        const dataFromBackend = reactive(data.map(item => ({...item, isVisible: false,})));

        function showTooltip(item) {
           const hoveredItemIndex = dataFromBackend.findIndex(a => a.day === item);
           dataFromBackend[hoveredItemIndex].isVisible = !dataFromBackend[hoveredItemIndex].isVisible;
        }

        const weekDays = ['sun', 'mon', 'tue', 'wed', 'thu', 'fri', 'sat'];
        const today = new Date().getDay();

        const isCurrentDay = computed(function() {
            return weekDays[today];
        })





        return {
            availableFunds,
            dataFromBackend,
            totalExpenses,
            showTooltip,
            isCurrentDay
        }

    }
    
}

</script>

<style scoped>
.container {
    min-width: 40%;
    max-width: 50rem;
    margin-right: auto;
    margin-left: auto;
}
.total-balance-container {
    background-color: var(--primary-soft-red);
    border-radius: 1rem;
    padding: 2rem 3rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.total-balance-info {
    color: var(--neutral-very-pale-orange);
    margin: 1rem;
}

.total-balance-title {
    font-weight: 400;
    margin-bottom: .5rem;
}

.total-balance-funds {
    font-size: 2.4rem;
    font-weight: 700;
}

.total-balance-icon img {
    width: 100%;
}

.chart-container {
    background-color: var(--neutral-very-pale-orange);
    border-radius: 10px;
    padding: 2rem 3rem;
    margin-top: 2rem;
}

.chart-container h3 {
    color: var(--neutral-dark-brown);
    margin-bottom: 4rem;
}

.data-container {
    display: flex;
    align-items: end;
    list-style: none;
    gap: .5rem;
}

.tooltip {
    width: 8rem;
    background-color: black;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 5px 0;
    position: absolute;
    top: -4rem;
    left: -2rem;
    z-index: 1;
}

.day-name {
    width: 4rem;
    color: var(--neutral-medium-brown);
    margin: 0 auto;
    text-align: center;
}

.chart-bar {
    border-radius: .5rem;
    background-color: var(--primary-soft-red);
    margin-bottom: 1rem;
}

.chart-bar:hover {
    cursor: pointer;
    opacity: .8;
}

.today {
    background-color: var(--primary-cyan);
}

hr {
    margin: 2rem auto;
    border-color: var(--neutral-very-pale-orange);
}

.total-expenses-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.expenses-total {
    font-size: 3.2rem;
    font-weight: 700;
    color: var(--neutral-dark-brown);
}

.expenses-diff {
    color: var(--neutral-dark-brown);
    font-weight: 700;
}

.expenses-text {
    color: var(--neutral-medium-brown);
}

.total-expenses-details {
    text-align: end;
}


</style>
