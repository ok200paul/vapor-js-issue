<template>
    <SecondaryButton>
        <label for="fileUpload" class="w-full cursor-pointer flex justify-center items-center ">
            <input type="file" id="fileUpload" name="fileUpload" ref="fileUpload" @change="upload"
                   class=" hidden">

            <div>
                <div class="flex justify-center items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                         stroke="currentColor" class="h-4 mr-2">
                        <path stroke-linecap="round" stroke-linejoin="round"
                              d="M9 8.25H7.5a2.25 2.25 0 0 0-2.25 2.25v9a2.25 2.25 0 0 0 2.25 2.25h9a2.25 2.25 0 0 0 2.25-2.25v-9a2.25 2.25 0 0 0-2.25-2.25H15m0-3-3-3m0 0-3 3m3-3V15"/>
                    </svg>


                    Upload {{ uploadType }}
                    <span v-if="uploadProgress" class="ml-2">
                        ({{ uploadProgress }}%)
                    </span>
                </div>

            </div>
        </label>
    </SecondaryButton>
</template>

<script setup>

import {ref} from "vue";
import SecondaryButton from "@/Components/SecondaryButton.vue";

const uploadProgress = ref(0);
const fileUpload = ref(null);

const emit = defineEmits(['uploadWasCompleted',])

const $props = defineProps({
    uploadType: {
        required: false,
        type: String,
        default: 'a resource'
    },
    folder: {
        required: true,
        type: String,
    },
    visibility: {
        required: false,
        type: String,
        default: 'private'
    },
    returnKeyOnly: {
        required: false,
        type: Boolean,
        default: false
    }
});

function upload() {

    let options = {
        progress: progress => {
            uploadProgress.value = Math.round(progress * 100);
        },
    };
    Vapor.store(fileUpload.value.files[0], options)
        .then(response => {
            console.log(response)
    });
}

</script>
