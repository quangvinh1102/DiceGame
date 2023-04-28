<template>
  <div class="wraper-popup" v-bind:class="getClassPopup">
    <div class="rule">
        <h3>Luật chơi</h3>
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Eos beatae corporis distinctio provident! Asperiores assumenda cumque quis explicabo quae rerum sit cum molestiae temporibus magni, perspiciatis sequi, eveniet obcaecati autem?</p>
    <button v-on:click="confirm">Đã hiểu</button>
    </div>
  </div>
</template>

<script>
export default {
    name: 'popup',
    data() {
        return {
            
        }
    },
    props: {
        isOpenpopup: Boolean
    },
    methods: {
        confirm() {
            this.$emit('handleConfirm')
        },
    },
    computed: {
        getClassPopup() {
            return this.isOpenpopup ? 'open-popup' : '';
        }
    }
}
</script>

<style>
.wraper-popup {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.5);
    opacity: 0;
    visibility: hidden;
    transition: all 0.5s ease-in-out;
}
.wraper-popup.open-popup {
    opacity: 1;
    visibility: visible;
}
.rule {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    width: 300px;
    height: 250px;
    top: 50%;
    left: 50%;
    position: absolute;
    transform: translate(-50%, -50%) scale(1.5);
    background-color: #fff;
    border-radius: 5px;
}
.wraper-popup button {
    width: 100px;
    height: 40px;
    background-color: rgb(91, 47, 47);
    color: white;
    font-size: 16px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
</style>