<script>
import Listitem from './ListItemComponent.vue'
export default{
    props:{
        data: {type: Array, required: true},
        changeStatus: {type: Boolean, required: false, default: false},
        canDelete: {type: Boolean, required: false, default: false}
    },
    methods:{
        changeDoneStatus(item) {
            this.$emit('onChangeStatus' , item)
        },
        deleteRecord(item) {
            this.$emit('onDelete', item)
        } 
    },
    components: {
    Listitem
}
}
</script>

<template>
    <ul>
        <Listitem 
            v-for="item in data"
            :key="item.index"
            :itemData="item"
            :renderCheckbox="changeStatus"
            :renderDeleteBtn="canDelete"
            @onChange="changeDoneStatus($event)"
            @onDelete="deleteRecord($event)"
        />
    </ul>
</template>