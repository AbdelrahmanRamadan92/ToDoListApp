<template>
    <div class="mt-3">
        <h2>add item form</h2>
        <div class="container m-2 w-100">
            <input
                type="test"
                placeholder="add item"
                class="border"
                v-model="item.name"
            />
            <button
                :class="[item.name ? 'active' : 'notactive']"
                @click="addItem()"
            >
                add +
            </button>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        };
    },
    methods: {
        addItem() {
            if (this.item.name == "") {
                return;
            }

            axios
                .post("http://127.0.0.1:8000/api/item/store", {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 201) {
                        this.item.name = "";
                        this.$emit("reloadlist");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    }
};
</script>

<style scoped>
.active {
    color: white;
    background-color: blue;
}
.inactive {
    color: gray;
}
</style>
