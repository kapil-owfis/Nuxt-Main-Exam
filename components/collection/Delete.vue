<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10">
      <TransitionChild
        as="template"
        enter="ease-out duration-300"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="ease-in duration-200"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div
          class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
        />
      </TransitionChild>

      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
        >
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          >
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-sm sm:p-6"
            >
            <button class="h-5 w-5 cursor-pointer" @click="emits('closeModal','delete')">
              <TrashIcon  />
            </button>
              <div>
                <div
                  class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-green-100"
                >
                  <CheckIcon
                    class="h-6 w-6 text-green-600"
                    aria-hidden="true"
                  />
                </div>
                <div class="mt-3 text-center sm:mt-5">
                  <DialogTitle
                    as="h3"
                    class="text-base font-semibold leading-6 text-gray-900"
                    >Are You Sure Want to Delete</DialogTitle
                  >
                  <div class="mt-2">
                    <p class="text-sm text-gray-500"></p>
                  </div>
                </div>
              </div>
              <div class="mt-5 flex justify-between">
                <button
                  type="button"
                  @click="emits('closeModal', 'delete')"
                  class="inline-flex w-full mr-3 justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                >
                  Cancel
                </button>
                <button
                  type="button"
                  @click="deleteCandidate"
                  class="inline-flex w-full justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                >
                  Delete
                </button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>
  
  <script setup lang="ts">
import { ref } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { CheckIcon } from "@heroicons/vue/24/outline";
import { TrashIcon } from "@heroicons/vue/20/solid";

const open = ref(true);
const emits = defineEmits(["deleteCandidate", "closeModal"]);

//candidate details props schema starts here
interface DeleteCandidateSchema {
  selectedCandidate: {
    name: string;
    age: string;
    dob: string;
    id: number;
  };
}
//candidate details props schema ends here

//defining props
const props = defineProps<DeleteCandidateSchema>();

const deleteCandidate = () => {
  emits("deleteCandidate", props.selectedCandidate);
};
</script>