<template>
    <div v-if="data.length > 0" :class="['container-body']">
        <ul :class="['container-list-body']" v-for="row in data" :key="row.id">
            <li :class="['container-list-item', { 'item-completed': row.flag }]">
                <strong :class="{ 'line-text': row.flag }"> 
                    <span v-if="editingId !== row.id">{{ row.description }}</span>
                    
                    <input 
                        v-else 
                        class="input-row" 
                        type="text" 
                        v-model="row.description" 
                        @keyup.enter="handleEdit(row)"
                        @blur="editingId = null"
                        v-focus
                    /> 
                </strong>
                <div>
                    <svg v-if="!row.flag && editingId !== row.id" @click="emit('confirmTodo', row)" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6" :class="['icon', 'icon-confirm']">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75 11.25 15 15 9.75M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                    </svg>

                    <svg v-if="row.flag && editingId !== row.id" @click="emit('confirmTodo', row)" :class="['icon', 'icon-toggle']" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                    </svg>

                    <strong v-if="!row.flag && editingId !== row.id">
                        <svg 
                            @click="startEdit(row.id)"
                            xmlns="http://www.w3.org/2000/svg" 
                            fill="none" 
                            viewBox="0 0 24 24" 
                            stroke-width="1.5" 
                            stroke="currentColor" 
                            class="size-6" 
                            :class="['icon', 'icon-settings']"
                        >
                            <path stroke-linecap="round" stroke-linejoin="round" d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L10.582 16.07a4.5 4.5 0 0 1-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 0 1 1.13-1.897l8.932-8.931Zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0 1 15.75 21H5.25A2.25 2.25 0 0 1 3 18.75V8.25A2.25 2.25 0 0 1 5.25 6H10" />
                        </svg>
                    </strong>

                    <strong v-if="!row.flag && editingId !== row.id">
                        <svg @click="emit('deleteTodo', row)" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6" :class="['icon', 'icon-delete']">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                        </svg>
                    </strong>
                </div>
            </li>
        </ul>
    </div>
</template>

<script setup>
     from 'vue';

    const emit = defineEmits(['deleteTodo', 'confirmTodo'])
    const props = defineProps({
        data: {
            type: Array,
            default: () => []
        }
    })

    const editingId = ref(null);

    const startEdit = (id) => {
        editingId.value = id;
    };

    const vFocus = {
        mounted: (el) => el.focus()
    };

    const handleEdit = (row) => {
        emit('settingsTodo', row);
        editingId.value = null;
    };
</script>

<style>
    .container-body {
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(10px);
        width: 490px;
        border-radius: 15px;
        padding: 20px 15px;
        border: none;
        box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        max-height: 400px;
        overflow-y: auto;
    }

    .container-body::-webkit-scrollbar {
        width: 8px;
    }

    .container-body::-webkit-scrollbar-track {
        background: #f1f1f1;
        border-radius: 10px;
    }

    .container-body::-webkit-scrollbar-thumb {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        border-radius: 10px;
    }

    .container-list-body {
        padding: 0;
        margin: 8px 0;
        list-style: none;
    }

    .container-list-item {
        border: none;
        background: linear-gradient(to right, #f8f9fa, #ffffff);
        padding: 14px 18px;
        border-radius: 10px;
        margin-bottom: 10px;
        font-size: 15px;
        color: #2d3748;
        transition: all 0.3s ease;
        border-left: 4px solid transparent;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .container-list-item:hover {
        transform: translateX(5px);
        box-shadow: 0 4px 12px rgba(102, 126, 234, 0.2);
        border-left: 4px solid #667eea;
        background: white;
    }

    .container-list-item:last-child {
        margin-bottom: 0;
    }

    .input-row {
        border: none;
        border-radius: 5px;
        padding: 3px;
        font-size: 15px;
        color: #2d3748;
        ;
    }

    .icon{
        width: 20px;
        height: 20px;
        transition: all 0.3s ease
    }

    .icon:hover {
        transform: translateY(-2px);
        cursor: pointer;
    }

    .icon-settings{
        color: rgb(162, 162, 236);
    }

    .icon-delete {
        color: rgb(245, 78, 78);
    }
    
    .icon-confirm {
        color: rgb(56, 155, 56);
    }
    .icon-toggle {
        color: rgb(236, 49, 16);
    }

    .line-text {
        text-decoration: line-through;
        color: gray;
    }
    .item-completed {
        background: linear-gradient(to right, #d4edda, #c3e6cb);
        border-left: 4px solid #28a745;
    }
</style>