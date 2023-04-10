<template>
  <div>
    <!--  pending block starts here-->
    <div v-if="pending">
      <div class="flex flex-1 flex-col p-8">
        <img
          class="mx-auto h-72 w-72 flex-shrink-0 rounded-full"
          :src="'https://cdn1.vectorstock.com/i/1000x1000/49/90/loading-icon-on-black-vector-24544990.jpg'"
          alt=""
        />
      </div>
    </div>
    <!-- pending block ends here -->

    <!-- add button start here -->

    <!-- add button start here -->
    <div class="flex justify-between">
      <input
        type="search"
        class="rounded"
        placeholder="search"
        @input="searchedCandidate"
        v-model="searchInput"
      />
      <button
        v-if="!pending"
        type="button"
        @click="isAdding = true"
        class="rounded-md bg-gray-950 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-gray-500"
      >
        Add Details
      </button>
    </div>
    <!-- candidate details cards starts here -->
    <div v-if="candidatesList && candidatesList.length && !isSearching">
      <div>
        <ul
          role="list"
          class="p-2 grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 h-full"
        >
          <li
            v-for="(candidate, index) in candidatesList"
            :key="index"
            class="col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow"
          >
            <div class="flex flex-1 flex-col p-8">
              <h3 class="mt-6 text-lg font-bold text-gray-900">
                Name:
                <span class="text-gray-900"> {{ candidate.name }}</span>
              </h3>
              <dl class="mt-1 flex flex-grow flex-col justify-between">
                <dd class="text-lg font-bold text-gray-900">
                  Age:
                  <span class="text-gray-900"> {{ candidate.age }}</span>
                </dd>
                <dd class="mt-3">
                  <a
                    class="rounded-full bg-white px-2 py-1 text-lg font-bold text-gray-800 cursor-pointer"
                  >
                    Date of Birth: <span> {{ candidate.dob }}</span>
                  </a>
                </dd>
              </dl>
            </div>
            <div>
              <div class="-mt-px flex divide-x divide-gray-200">
                <div
                  class="flex w-0 flex-1 cursor-pointer"
                  @click="updateselectedCandidate(candidate)"
                >
                  <a
                    class="relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
                  >
                    <PencilIcon
                      class="h-5 w-5 text-gray-400"
                      aria-hidden="true"
                    />
                    Edit
                  </a>
                </div>
                <div
                  class="-ml-px flex w-0 flex-1 cursor-pointer"
                  @click="deleteselectedCandidate(candidate)"
                >
                  <a
                    class="relative inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-br-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
                  >
                    <TrashIcon
                      class="h-5 w-5 text-gray-400"
                      aria-hidden="true"
                    />
                    Delete
                  </a>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
      <div></div>
    </div>
    <!-- candidate details  cards ends here -->

<!-- searched details here -->
<div v-if="searchedDetails && searchedDetails.length && isSearching">
      <div>
        <ul
          role="list"
          class="p-2 grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 h-full"
        >
          <li
            v-for="(candidate, index) in candidatesList"
            :key="index"
            class="col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow"
          >
            <div class="flex flex-1 flex-col p-8">
              <h3 class="mt-6 text-lg font-bold text-gray-900">
                Name:
                <span class="text-gray-900"> {{ candidate.name }}</span>
              </h3>
              <dl class="mt-1 flex flex-grow flex-col justify-between">
                <dd class="text-lg font-bold text-gray-900">
                  Age:
                  <span class="text-gray-900"> {{ candidate.age }}</span>
                </dd>
                <dd class="mt-3">
                  <a
                    class="rounded-full bg-white px-2 py-1 text-lg font-bold text-gray-800 cursor-pointer"
                  >
                    Date of Birth: <span> {{ candidate.dob }}</span>
                  </a>
                </dd>
              </dl>
            </div>
            <div>
              <div class="-mt-px flex divide-x divide-gray-200">
                <div
                  class="flex w-0 flex-1 cursor-pointer"
                  @click="updateselectedCandidate(candidate)"
                >
                  <a
                    class="relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
                  >
                    <PencilIcon
                      class="h-5 w-5 text-gray-400"
                      aria-hidden="true"
                    />
                    Edit
                  </a>
                </div>
                <div
                  class="-ml-px flex w-0 flex-1 cursor-pointer"
                  @click="deleteCandidate(candidate)"
                >
                  <a
                    class="relative inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-br-lg border border-transparent py-4 text-sm font-semibold text-gray-900"
                  >
                    <TrashIcon
                      class="h-5 w-5 text-gray-400"
                      aria-hidden="true"
                    />
                    Delete
                  </a>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
      <div></div>
    </div>

<!-- searched details here -->
    <!-- and and edit slide bar starts  here -->
    <div>
      <!-- Add modal starts here -->
      <CollectionAdd
        v-if="isAdding"
        @addCandidate="addCandidateDetalis"
        @closeModal="closeModal"
      />
      <!-- add modal ends here -->

      <!-- edit modal stars here -->
      <CollectionEdit
        v-if="isEditing"
        :selectedCandidate="selectedCandidate"
        @updateDetails="updateDetails"
        @closeModal="closeModal"
      />
      <!-- edit modal ends here -->
      <!-- delte modal -->
        <CollectionDelete  v-if="isDeleting" :selectedCandidate="selectedCandidate" @deleteCandidate="deleteCandidate"/>
      <!-- delte modal -->
    </div>
    <!-- and and edit slide bar ends here -->
    <!-- No Candidate details starts here -->
    <div v-if="candidatesList && candidatesList.lenth">
      <div class="flex flex-col items-center">
        <img
          class="h-72 w-72 mb-4"
          src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRU3rUmjOvvo41Ga_G44WjcenlHmAJhBZpWtg&usqp=CAU"
        />
        <h1 class="text-2xl font-bold">No Candiate Details Found</h1>
      </div>
    </div>
    <!-- No Candidate details ends here -->
  </div>
</template>
      
      <script setup lang="ts">
import { PencilIcon, TrashIcon } from "@heroicons/vue/20/solid";
import { loadConfig } from "c12";

//varialbe declarations starts here
const candidatesList: any = ref([]);
const isAdding: any = ref(false);
const isEditing: any = ref(false);
const pending: any = ref(true);
const selectedCandidate: any = ref();
let indexOfSelected;
const searchInput: any = ref("");
const searchedDetails: any = ref([]);
const isSearching:any= ref(false)
const isDeleting:any= ref(false)
//varialbe declarations ends here

//getting candidate details on mounted starts here
onMounted(async () => {
  await getCandidateDetails();
});
// getting candidate details  on mounted ends here

//finding the index of candidate  starts here
const getIndexOfSelected = (id: any) => {
  let index = candidatesList.value.findIndex((item: any) => item.id == id);
  return index;
};
// finding the index of candidate ends here

// set selected candidate  to selectedCandidate starts here
const updateselectedCandidate = (candidate: any) => {
  selectedCandidate.value = candidate;
  isEditing.value = true;
};
// set selected candidate  to selectedCandidate starts here

const deleteselectedCandidate = (candidate: any) => {
  selectedCandidate.value = candidate;
  isDeleting.value = true;
};


//getting  candidate details starts here
const getCandidateDetails = async () => {
  let data: any = localStorage.getItem("candidateDetails");
  candidatesList.value = JSON.parse(data);
  pending.value = false;
};
//getting candidate details ends here

//local storage
const updateLocalStorage = () => {
  localStorage.setItem(
    "candidateDetails",
    JSON.stringify(candidatesList.value)
  );
};
//local storage ends here

//  adding candidate to local storage starts here
const addCandidateDetalis = async (candidate: any) => {
  candidate.id = candidatesList.value.length;
  candidatesList.value.unshift(candidate);
  updateLocalStorage();
  isAdding.value = false;
};
//adding candidate to local storage ends  here

// updating candidate details starts here
const updateDetails = async (candidate: any) => {
  indexOfSelected = getIndexOfSelected(candidate.id);
  candidatesList.value[indexOfSelected] = candidate;
  updateLocalStorage();
  isEditing.value = false;
};
//updating candidate details ends  here

//delete candidate starts here
const deleteCandidate = async (candidate: any) => {   
  isDeleting.value=false     
  //to get the index of candidate
  indexOfSelected = getIndexOfSelected(candidate.id);
  candidatesList.value.splice(indexOfSelected, 1);
  updateLocalStorage();
};
//delete call ends here

//closing add or edit modal
const closeModal = (value: any) => {
  if (value == "edit") isEditing.value = false;
  else if(value=='delete') isDeleting.value=false
  isAdding.value = false;
};

const searchedCandidate = (searchInput: any) => {
  if (searchInput.data != "") {
    let array = candidatesList.value.filter((candidate: any) => {
      return candidate.name
        .toLowerCase()
        .includes(searchInput.data.toLowerCase());
    });
      if (array.length == 0) {
        searchedDetails.value = candidatesList.value;
        isSearching.value=false
      }
      searchedDetails.value = array;
      isSearching.value=true
  }
  else{
    searchedDetails.value=candidatesList.value
    isSearching.value=false
  }
};
</script>