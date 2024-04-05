<scipt>
    export default {
        name: "LessonsForm"
    }
</scipt>
<script setup>
import FormSection from '@/Components/FormSection.vue'
import InputError from '@/Components/InputError.vue'
import InputLabel from '@/Components/InputLabel.vue'
import PrimaryButton from '@/Components/PrimaryButton.vue'
import TextInput from '@/Components/TextInput.vue'
import SecondaryButton from '@/Components/SecondaryButton.vue'
import CollectionSelector from '../Common/CollectionSelector.vue'
import { ref } from 'vue'
defineProps({
    form: {
        type: Object,
        required: true
    },
    updating: {
        type: Boolean,
        required: false,
        default: false
    },
    categories: {
        type: Object,
        required: true
    },
    levels: {
        type: Object,
        required: true
    }
})
const categoriesSelected = ref([])
const onCategories = (_categories) => {
    categoriesSelected.value = _categories
}
defineEmits(['submit'])
</script>

<template>
    <FormSection @submitted="$emit('submit')">
        <template #title>
            {{ updating ? "Update Lesson" : "Create New Lesson" }}
        </template>

        <template #description>
            {{ updating ? "Update the selected lesson" : "Create a new lesson from scratch" }}
        </template>
        <template #form>
            <div class="col-span-6 sm:col-span-6">
                <!-- name -->
                <InputLabel for="name" value="Name" />
                <TextInput id="name" type="text" v-model="form.name" autocomplete="name" class="mt-1 block w-full" />
                <InputError :message="$page.props.errors.name" class="mt-2" />
                <br />
                <!-- description -->
                <InputLabel for="description" value="Description" />
                <TextInput id="description" type="text" v-model="form.description" autocomplete="description"
                    class="mt-1 block w-full" />
                <InputError :message="$page.props.errors.description" class="mt-2" />
                <br />
                <!-- content -->
                <InputLabel for="content_uri" value="Content" />
                <TextInput id="content_uri" type="text" v-model="form.content_uri" autocomplete="content_uri"
                    class="mt-1 block w-full" />
                <InputError :message="$page.props.errors.content_uri" class="mt-2" />
                <br />
                <!-- pdf -->
                <InputLabel for="pdf_uri" value="Upload the file" />
                <SecondaryButton class="mt-2 mr-2" type="button">Upload PDF</SecondaryButton>
                <InputError :message="$page.props.errors.pdf_uri" class="mt-2" />
                <br />
                <div class="w-full">
                    <div class="flex">
                        <div class="w-1/2">
                            <!-- level -->
                            <InputLabel for="level_id" value="Level" />
                            <select class="w-4/5 px-auto rounded">
                                <option v-for="level in levels" :value="level.id">{{ level.name }}</option>
                            </select>
                            <InputError :message="$page.props.errors.level_id" class="mt-2" />
                        </div>
                        <div class="w-1/2">
                            <!-- categories -->
                            <InputLabel for="categories" value="Categories" />
                            <CollectionSelector :name="categories" :id="categories" :collection="categories"
                                @onCategories="onCategories">
                            </CollectionSelector>
                        </div>
                    </div>
                </div>
            </div>
        </template>
        <template #actions>
            <PrimaryButton @click="$emit('submit')">
                {{ updating ? "Update Lesson" : "Create Lesson" }}
            </PrimaryButton>
        </template>
    </FormSection>
</template>