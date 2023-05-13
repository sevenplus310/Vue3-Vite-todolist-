<template>
    <div class="eventView">
        <input type="checkbox" name="" id="" @change="onDeleteEvent">
        <div class="event-right">
            <h3 class="title">{{ event.eventName }}</h3>
            <div class="eventDetails">
                <div class="alterTime">
                    <img src="./icons/alter.svg" alt="">
                    <p class="time">{{ event.eventTime }}</p>
                </div>
                <div class="date">
                    <img src="./icons/date.svg" alt="">
                    <p class="time">{{ event.eventDate }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {defineProps} from 'vue'

const props=defineProps({
    event:{
        type:Object,
        required:true
    }
});

const emit = defineEmits(['delete-event']);

function onDeleteEvent(event) {
if(event.target.checked){
    emit('delete-event',props.event.id)
}
}


</script>

<style scoped>
.title {
    /* material-theme/title/medium */

    font-family: 'Roboto';
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */

    display: flex;
    align-items: center;
    text-align: center;

    /* material-theme/sys/light/on-surface */

    color: var(--on-surface);


    /* Inside auto layout */

    flex: none;
    order: 0;
    flex-grow: 0;
}

.eventView {
    /* eventView */


    /* 自动布局 */

    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 16px;
    gap: 16px;

    width: 358px;
    height: 72px;

    /* material-theme/sys/light/surface */

    background: #FBF8FD;
    opacity: 0.9;
    backdrop-filter: blur(15px);
    /* Note: backdrop-filter has minimal browser support */

    border-radius: 16px;
}


.event-right {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 0px;
    gap: 4px;

    width: 286px;
    height: 40px;


    /* Inside auto layout */

    flex: none;
    order: 1;
    flex-grow: 1;
}



.eventDetails {
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 0px;
    gap: 16px;

    width: 306px;
    height: 12px;


    /* Inside auto layout */

    flex: none;
    order: 1;
    align-self: stretch;
    flex-grow: 0;
}



.date {
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 0px;
    gap: 4px;

    width: 74px;
    height: 12px;


    /* Inside auto layout */

    flex: none;
    order: 0;
    flex-grow: 0;
}

.alterTime {
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 0px;
    gap: 4px;
    width: 74px;
    height: 12px;


    /* Inside auto layout */

    flex: none;
    order: 0;
    flex-grow: 0;
}

.time {
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 500;
    font-size: 12px;
    line-height: 16px;
    leading-trim: both;
    text-edge: cap;
    display: flex;
    align-items: center;
    text-align: center;

    /* material-theme/sys/light/on-surface */

    color: var(--on-surface);


    /* Inside auto layout */

    flex: none;
    order: 1;
    flex-grow: 0;
}
</style>