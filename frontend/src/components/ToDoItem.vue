<template>
    <li class="list-group-item d-flex justify-content-between w-50">
        <input type="checkbox" @change="updateCheck()" class="mr-3" />
        <span :class="[item.completed ? 'completed' : '', 'item']">
            {{ item.name }}
        </span>
        <button class="btn-danger ml-3" @click="removeItem()">X</button>
    </li>
</template>

<script>
import axios from 'axios'
export default {
    props: ["item"],
    methods: {
        updateCheck() {
            axios
                .put(`http://127.0.0.1:8000/api/item/${this.item.id}`, {
                    item: this.item
                })
                .then(res => {
                    console.log(res);
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios put", error);
                });
        },
        removeItem() {
            axios
                .delete(`http://127.0.0.1:8000/api/item/${this.item.id}`)
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios delte ", error);
                });
        }
    }
}; 
</script>

<style>
.completed {
    text-decoration: line-through;
    color: gray;
}

.item {
    word-break: break-all;
}
</style>
