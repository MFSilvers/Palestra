<script setup lang="ts">
import { computed } from 'vue';
import { Check } from 'lucide-vue-next';
import { cn } from '@/lib/utils';

interface Props {
    modelValue?: boolean;
    class?: string;
}

const props = withDefaults(defineProps<Props>(), {
    modelValue: false,
});

const emit = defineEmits<{
    (e: 'update:modelValue', value: boolean): void;
}>();

const checked = computed({
    get: () => props.modelValue,
    set: (value: boolean) => emit('update:modelValue', value),
});
</script>

<template>
    <button
        type="button"
        role="checkbox"
        :aria-checked="checked"
        :data-state="checked ? 'checked' : 'unchecked'"
        :class="
            cn(
                'peer h-4 w-4 shrink-0 rounded-sm border border-primary ring-offset-background focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-50 data-[state=checked]:bg-primary data-[state=checked]:text-primary-foreground',
                props.class
            )
        "
        @click="checked = !checked"
    >
        <Check v-if="checked" class="h-4 w-4" />
    </button>
</template> 