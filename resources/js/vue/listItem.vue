<template>
    <div class="item">
        <input type="checkbox" @change="updateCheck()" v-model="item.completed">
        <span :class="[item.completed ? 'completed' : '', 'itemText']"> {{ item.name }} </span>
        <button @click="removeItem()" type="submit" class="btn btn-danger"> Delete </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods:{
        updateCheck(){
            axios.put('/api/item/'+this.item.id, {item:this.item})
                .then(res => {
                    if(res.status == 200){
                        this.$emit('itemChanged');
                    }
                })
                .catch(err => {
                    console.log(err);
                })
        }, 

        removeItem(){
            axios.delete('/api/item/'+this.item.id)
                 .then(res => {
                     if(res.status == 200){
                         this.$emit('itemChanged');
                     }
                 })
                 .catch(err => {
                     console.log(err);
                 })
        }
    }
}   
</script>

<style scoped>
    .completed{
        text-decoration: line-through;
        color: rgb(36, 37, 37);
    }
    .itemText{
        width: 100%;
        margin-left: 20px;
    }
    .item{
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 10px;
    }
</style>