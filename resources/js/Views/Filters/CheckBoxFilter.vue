<script setup>
import { onMounted, ref, watch } from 'vue';
import { Checkbox } from "@/Components/shadcn/ui/checkbox/index.js";
import { Switch } from "@/Components/shadcn/ui/switch/index.js";
import { useUtilities } from "@/Composables/useUtilities.js";

const props = defineProps({
    items: {
        type: Array,
        required: true
    },
    title: {
        type: String,
        required: true
    },
    icon: {
        type: Object,
        required: true
    },
    showColorBadge: {
        type: Boolean,
        default: false,
    },
    initialCheckedItems: {
        type: Array,
        default: () => []
    }
});

const emit = defineEmits(['update:checked']);
const utilities = useUtilities();
const allChecked = ref(false);
const checkedItems = ref([]);

// Initialize checkedItems with persisted data
onMounted(() => {
    checkedItems.value = props.items.map(item => {
        const isChecked = props.initialCheckedItems.some(checkedItem => {
            return String(checkedItem.name) === String(item.name);
        });
        return { ...item, checked: isChecked };
    });
    // Set allChecked if all items are initially checked
    allChecked.value = checkedItems.value.every(item => item.checked);
});

const toggleAll = (checked) => {
    allChecked.value = checked;
    checkedItems.value.forEach(item => item.checked = checked);
    emitCheckedItems();
};

const toggleItem = (item) => {
    item.checked = !item.checked;
    // Update allChecked state based on checkedItems
    allChecked.value = checkedItems.value.every(item => item.checked);
    emitCheckedItems();
};

const emitCheckedItems = () => {
    const selectedItems = checkedItems.value.filter(item => item.checked).map(item => ({id: item.id, name: item.name}));
    emit('update:checked', selectedItems, utilities.toCamelCase(props.title));
};
</script>

<template>
    <div class="flex flex-col space-y-2 text-sm">
        <div class="flex w-full items-center space-x-1 pt-3">
            <component :is="icon" size="17"/>
            <div class="font-medium text-base">{{ title }}</div>
        </div>
        <div class="flex flex-col space-y-3">
            <div class="flex items-center justify-between p-2 rounded-lg bg-slate-100">
                <div>All {{ title }}'s</div>
                <Switch v-model:checked="allChecked" @update:checked="toggleAll"/>
            </div>
            <div v-for="item in checkedItems" :key="item.id" class="flex items-center space-x-2 w-full pl-1">
                <div class="flex space-x-2 items-center w-9/12">
                    <Checkbox class="w-3.5 h-3.5" :checked="item.checked" @update:checked="() => toggleItem(item)"/>
                    <div class="flex items-center space-x-1">
                        <div v-if="showColorBadge" class="min-w-4 h-4 rounded-full border border-gray-300"
                             :style="{ backgroundColor: item.hex }"></div>
                        <span class="capitalize">{{ utilities.removeUnderscores(item.name) }}</span>
                    </div>
                </div>
                <div class="text-center bg-gray-100 px-3 py-0.5 rounded-lg">1712</div>
            </div>
        </div>
    </div>
</template>

<style scoped>
/* Your styles here */
</style>
