<template>
  <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10">
      <div class="fixed inset-0" />

      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div
            class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16"
          >
            <TransitionChild
              as="template"
              enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full"
              enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700"
              leave-from="translate-x-0"
              leave-to="translate-x-full"
            >
              <DialogPanel class="pointer-events-auto w-screen max-w-2xl">
                <div
                  class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                >
                  <div class="px-4 sm:px-6">
                    <div class="flex items-start justify-between">
                      <DialogTitle
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Update  Details</DialogTitle
                      >
                      <div class="ml-3 flex h-7 items-center">
                        <button
                          type="button"
                          class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                          @click="open = false"
                        >
                          <XMarkIcon
                            @click="emits('closeModal', 'edit')"
                            class="h-6 w-6"
                            aria-hidden="true"
                          />
                        </button>
                      </div>
                    </div>
                  </div>
                    <!-- update candidate details starts here -->
                  <div class="relative mt-6 flex-1 px-4 sm:px-6">
                    <!-- candidate name starts here -->

                    <div class="mt-2 mb-3">
                      <label
                        for="name"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Name</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="candidate.name"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="name"
                        placeholder="Enter Name"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- candidate name ends here -->
                    <!-- candidate age  starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="age"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Age</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="candidate.age"
                        type="textarea"
                        oninvalid="Enter at least 5 characters"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="age"
                        placeholder="Enter age"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- candidate age ends here -->

                    <!-- candidate  date of birth starts here -->
                    <div class="mt-2 mb-3">
                      <label
                        for="dateOfBirth"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Date Of Birth</label
                      >
                      <input
                        ref="text_input_ref"
                        v-model="candidate.dob"
                        type="date"
                        aria-describedby="input-live-help input-url-feedback"
                        autofocus
                        id="dateOfBirth"
                        class="block w-full mt-2 rounded-md border-0 text-gray-900 shadow-sm p-[8px] ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 focus-visible:ring-2 sm:text-sm sm:leading-6 focus-within:outline-none focus-visible:outline-none focus-visible:shadow-none focus-visible:ring-indigo-600"
                      />
                    </div>
                    <!-- candidte date of birth ends here-->
                  </div>
                  <!-- update candidate details ends here -->


                  <!-- candidate gender starts here -->
                  <div class="mt-2 mb-3">
                      <label
                        for="dateOfBirth"
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Gender</label
                      >
                      <select
                        v-model="candidate.gender"
                        id="type"
                        class="block w-full mt-2 rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      >
                        <option value="Male">Male</option>
                        <option value="Female">Female</option>
                      </select>
                    </div>

                  <!-- candidate gender ends here -->
                  <!-- update and cancel  buttons starts here -->
                  <div class="mt-5 flex justify-between">
                    <button
                      type="button"
                      @click="emits('closeModal','edit')"
                      class="inline-flex w-full mr-3 justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      Cancel
                    </button>
                    <button
                      type="button"
                      @click="updateDetails"
                      class="inline-flex w-full justify-center rounded-md bg-slate-900 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-slate-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      update 
                    </button>
                  </div>
                  <!-- add and cancel buttons ends here -->
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
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
import { XMarkIcon } from "@heroicons/vue/24/outline";

const open = ref(true);

//defining emits
const emits = defineEmits(["updateDetails", "closeModal"]);

//candidate details props schema starts here
interface UpdateCandidateSchema {
    selectedCandidate: {
    name: string;
    age: string;
    dob:string,
    gender:string,
    id:number
  };
}
//candidate details props schema ends here

//defining props
const props = defineProps<UpdateCandidateSchema>()

//builder details object
const candidate = ref({
  name: props.selectedCandidate.name,
  age:props.selectedCandidate.age,
  dob: props.selectedCandidate.dob,
  gender:props.selectedCandidate.gender,
  id:props.selectedCandidate.id
});

//emitting the builder details
const updateDetails = () => {
    emits("updateDetails", candidate.value);
};
</script>