<script setup>
import {onMounted, ref, watch} from "vue";
import {useUtilities} from "@/Composables/useUtilities.js";
import {Input} from "@/Components/shadcn/ui/input/index.js";

const props = defineProps({
    title: {
        type: String,
        required: true
    },
    inputPlaceholder: {
        type: String,
        default: "From"
    },
    inputPlaceholder2: {
        type: String,
        default: "To"
    },
    icon: {
        type: Object,
        required: true
    },
    initialFrom: {
        type: String,
        default: null
    },
    initialTo: {
        type: String,
        default: null
    }
})

const emit = defineEmits(['update:range']);

const selectedFrom = ref(null);
const selectedTo = ref(null);

onMounted(() => {
    selectedFrom.value = props.initialFrom;
    selectedTo.value = props.initialTo;
});

watch([selectedFrom, selectedTo], ([newFrom, newTo]) => {
    console.log("selectedFrom: ", newFrom);
    console.log("selectedTo: ", newTo);
    emit('update:range', {from: newFrom, to: newTo}, useUtilities().toCamelCase(props.title));
});
</script>

<template>
    <div class="flex flex-col space-y-2 py-4 w-full">
        <div class="flex w-full items-center space-x-1">
            <component :is="icon" size="17"/>
            <div class="font-medium text-base">{{title}}</div>
        </div>
        <div class="flex w-full space-x-2">
            <Input v-model="selectedFrom" :placeholder="inputPlaceholder" class="text-sm md:w-32 h-8 border border-gray-900 rounded-sm px-2"/>
            <span>-</span>
            <Input v-model="selectedTo" :placeholder="inputPlaceholder2" class="border border-gray-900 rounded-sm px-2 text-sm md:w-32 h-8"/>
        </div>
    </div>
</template>

<style scoped>

</style>
