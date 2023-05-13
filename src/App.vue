<template>
    <div class="seeView">
        <div class="mask-backgronded">
            <h2>TodoLists</h2>
            <div class="contain">
                <eventView v-for="event in events" :key='event.id' :event="event" @delete-event="deleteEvent(event.id)" />
            </div>
            <addVue @add-event="addEvent" />
        </div>
    </div>
</template>


<script setup>
import { ref } from 'vue';
import eventView from './components/eventView.vue';
import addVue from './components/add.vue';

const events = ref([
    {
        id: 0,
        eventName: 'Event 1',
        eventTime: '10:00',
        eventDate: '2023-05-12'
    },
    {
        id: 1,
        eventName: 'Event 2',
        eventTime: '14:00',
        eventDate: '2023-05-13'
    },
    {
        id: 2,
        eventName: 'Event 3',
        eventTime: '18:00',
        eventDate: '2023-05-15'
    }
]);

function addEvent(newData) {
    events.value.push({
        id: events.value.length,
        eventName: newData.eventName,
        eventTime: newData.eventTime,
        eventDate: newData.eventDate,
    });
}

const emit = defineEmits(['delete-event'])

function deleteEvent(id) {
    events.value = events.value.filter(event => event.id !== id);
    emit('delete-event', id);
}
</script>

<style scoped>
.mask-backgronded {
    /* mask-backgronded */
    position: relative;
    height: 845px;
    background-image: url("./components/icons/bg.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    border-radius: 16px;
    display: flex;
    /* 添加flex布局 */
    flex-direction: column;
    /* 主轴为垂直方向，起点在上沿 */
    justify-content: center;
    /* 在主轴方向上居中 */
    align-items: center;
    /* 在交叉轴方向上居中 */

}

h2 {
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 500;
    font-size: 32px;
    line-height: 48px;
    /* identical to box height, or 150% */

    display: flex;
    align-items: center;
    text-align: center;

    /* material-theme/sys/light/on-surface */

    color: var(--on-surface);
    text-shadow: 0px 4px 4px rgba(188, 185, 185, 0.418);
}

.seeView {
    /* seeView */


    /* 自动布局 */

    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 8px;

    position: absolute;
    width: 390px;
    height: 845px;
    left: calc(50% - 390px/2);
}

.contain {

    display: flex;
    padding: 8px 0px;
    gap: 8px;
    width: 390px;
    height: 644px;
    align-content: center;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
}
</style>