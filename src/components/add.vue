<template>
    <div>
        <div class="box" @click="openDialog">
            <img src="./icons/add.svg" alt="">
            <p class="title">添加任务</p>
        </div>

        <div class="popup-box" v-if="showDialog">
            <div class="popup-mask" @click="closeDialog">
                <div class="popup-content" @click.stop>
                    <div class="popup-crtl">
                        <img class="cancel" src="./icons/x-circle.svg" alt="" @click="closeDialog">
                        <div class="input">
                            <input type="text" placeholder="请输入事件" v-model="eventName" @input="checkedInput">
                            <input type="time" placeholder="请选择时间" v-model="eventTime" @input="checkedInput">
                            <input type="date" placeholder="请选择日期" v-model="eventDate" @input="checkedInput">
                        </div>
                        <button class="confirm" type="submit" @click="handleAddEvent" :disabled="!isConfirmEnabled"
                            :class="{ 'disable-background-color': !isConfirmEnabled }">确认</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const emit = defineEmits(['add-event']);

function useDialog() {
    const showDialog = ref(false);
    const eventName = ref('');
    const eventTime = ref('');
    const eventDate = ref('');

    function closeDialog() {
        showDialog.value = false
        eventName.value = '';
        eventTime.value = '';
        eventDate.value = '';
    };

    function openDialog() {
        showDialog.value = true
    };

    function handleAddEvent() {
        const newData = {
            eventName: eventName.value,
            eventTime: eventTime.value,
            eventDate: eventDate.value,
        };
        emit('add-event', newData);
        closeDialog()
    }

    const isConfirmEnabled = computed(() => {
        return eventName.value.trim() !== '' && eventTime.value.trim() !== '' && eventDate.value.trim() !== '';
    });

    function checkedInput() {
    }

    return {
        showDialog,
        openDialog,
        closeDialog,
        eventName,
        eventTime,
        eventDate,
        handleAddEvent,
        isConfirmEnabled,
        checkedInput
    }
}

const { showDialog, openDialog, closeDialog, eventName, eventTime, eventDate, handleAddEvent, isConfirmEnabled, checkedInput } = useDialog();



</script>


<style scoped>
.box {
    /* 自动布局 */

    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 16px;
    gap: 8px;

    width: 358px;
    height: 56px;

    /* material-theme/sys/light/surface */

    background: #FBF8FD;
    opacity: 0.9;
    box-shadow: 0px 4px 80px rgba(0, 0, 0, 0.25);
    border-radius: 16px;

    /* Inside auto layout */

    flex: none;
    order: 1;
    align-self: stretch;
    flex-grow: 0;
}

.title {
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* or 150% */

    /* leading-trim and text-edge are draft CSS properties.

Read more: https://drafts.csswg.org/css-inline-3/#leading-trim
*/
    leading-trim: both;
    text-edge: cap;
    display: flex;
    align-items: center;
    text-align: center;

    /* material-theme/sys/light/primary */

    color: #1B59C3;


    /* Inside auto layout */

    flex: none;
    order: 1;
    flex-grow: 0;
}

.popup-box {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 16px;
    gap: 10px;

    position: absolute;
    width: 40%;
    height: 100%;
    left: calc(50% - 390px/2);
    bottom: 0px;

    /* material-theme/sys/light/surface */

    background: var(surface);
    border-radius: 32px 32px 0px 0px;
}


.popup-mask {
    background-color: rgba(0, 0, 0, 0.5);
    position: fixed;
    z-index: 90;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 99;
}

.popup-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 18px;
    gap: 32px;

    position: absolute;
    width: 390px;
    height: 46%;
    left: calc(50% - 390px/2);
    bottom: 0px;

    /* material-theme/sys/light/surface */

    background: #FBF8FD;
    border-radius: 32px 32px 0px 0px;
    z-index: 100;
}

.input {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px 0px;
    gap: 16px;

    width: 358px;
    height: auto;


    /* Inside auto layout */

    flex: none;
    order: 1;
    align-self: stretch;
    flex-grow: 0;
}

input {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    width: 100%;
    height: 52px;
    padding: 14px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 16px;
    margin-bottom: 10px;
}

.cancel {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;

    width: 194%;
    height: 24px;

}

.confirm {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 16px;
    width: 100%;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 16px;
    margin-bottom: 10px;
    background-color: #1B59C3;
    color: #fff;
    
}

.disable-background-color {
    background-color: #ccc;
}
</style >