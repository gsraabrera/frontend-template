<template>
  <div class="w-full">
    <div class="flex justify-end content-start ml-20 top-10 right-5 absolute">
      <button 
          v-if="!editable  && input.is_active === false"
          class="bg-transparent mr-3 py-3 px-3 border-2 hover:border-gray-400 text-green-500 font-bold content-center flex items-start rounded-full focus:outline-none focus:shadow-outline w-10 h-10" 
          type="button"
          data-tooltip-title="Activate"
          @click="actionWithConfirmation('activate')"
        >
        <font-awesome-icon :icon="['fas', 'toggle-off']" class="icon alt"/>
      </button>  
      <button 
          v-if="!editable  && input.is_active === true"
          class="bg-transparent mr-3 py-3 px-3 border-2 hover:border-gray-400 text-green-500 font-bold content-center flex items-start rounded-full focus:outline-none focus:shadow-outline w-10 h-10" 
          type="button"
          data-tooltip-title="Deactivate"
          @click="actionWithConfirmation('deactivate')"
          
        >
        <font-awesome-icon :icon="['fas', 'toggle-on']" class="icon alt"/>
      </button> 
      <button 
          v-if="!editable && input.is_verified === false"
          class="bg-transparent mr-3 py-3 px-3 border-2 hover:border-gray-400 text-green-500  font-bold content-center flex items-start rounded-full focus:outline-none focus:shadow-outline w-10 h-10" 
          type="button"
          data-tooltip-title="Verify"
          @click="actionWithConfirmation('verify')"
        >
        <font-awesome-icon :icon="['fas', 'check']" transform="shrink-6" mask="shield" class="icon alt"/>
      </button>
      <button 
          v-if="!editable && input.is_verified === true"
          class="bg-transparent mr-3 py-3 px-3 border-2 hover:border-gray-400 text-green-500  font-bold content-center flex items-start rounded-full focus:outline-none focus:shadow-outline w-10 h-10" 
          type="button"
          data-tooltip-title="Unverify"
          @click="actionWithConfirmation('unverify')"
        >
        <font-awesome-icon :icon="['fas', 'x']" transform="shrink-6" mask="shield" class="icon alt"/>
      </button>
      <button 
          v-if="!editable"
          class="w-10 h-10 mr-3 bg-transparent border-2 border-grey-200 hover:border-green-500  text-green-500 font-bold px-3 rounded-full focus:outline-none focus:shadow-outline" 
          type="button"
          @click="clickMakeEditable()"
        >
        <font-awesome-icon :icon="['fas', 'pencil']" class="icon alt"/>
      </button> 
      <button 
          v-if="!editable"
          class="bg-transparent py-3 px-3 border-2 hover:border-gray-400 text-white font-bold content-center flex items-start rounded-full focus:outline-none focus:shadow-outline w-10 h-10" 
          type="button"
          @click="closeDrawer()"
        >
        <svg id="Capa_1" fill="gray" height="15px" width="15px" version="1.1"  xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 460.775 460.775" xml:space="preserve"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M285.08,230.397L456.218,59.27c6.076-6.077,6.076-15.911,0-21.986L423.511,4.565c-2.913-2.911-6.866-4.55-10.992-4.55 c-4.127,0-8.08,1.639-10.993,4.55l-171.138,171.14L59.25,4.565c-2.913-2.911-6.866-4.55-10.993-4.55 c-4.126,0-8.08,1.639-10.992,4.55L4.558,37.284c-6.077,6.075-6.077,15.909,0,21.986l171.138,171.128L4.575,401.505 c-6.074,6.077-6.074,15.911,0,21.986l32.709,32.719c2.911,2.911,6.865,4.55,10.992,4.55c4.127,0,8.08-1.639,10.994-4.55 l171.117-171.12l171.118,171.12c2.913,2.911,6.866,4.55,10.993,4.55c4.128,0,8.081-1.639,10.992-4.55l32.709-32.719 c6.074-6.075,6.074-15.909,0-21.986L285.08,230.397z"></path> </g></svg>
      </button>
    </div>

    <div class="max-w-xs mt-2"> 
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
          First Name
        </label>
        <input 
          v-model="input.first_name"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
          :disabled="!editable"
          type="text"
        >
      </div>
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
          Middle Name
        </label>
        <input 
        v-model="input.middle_name"
        class="mt-2 shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" 
        :disabled="!editable"
        type="text"
        >
      </div>
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
          Last Name
        </label>
        <input 
        v-model="input.last_name"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" 
        :disabled="!editable"
        type="text"
        >
      </div>
      <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
             Sex
          </label>
          <!-- <input 
          v-model="input.sex"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
          :disabled="!editable"
          type="text"
          > -->
        <select 
        v-model="input.sex"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" 
        :disabled="!editable"
        label="Please select"
        >
             <!-- <option disabled value="">Please select</option> -->
             <option class="py-2 px-3 text-gray-700">Male</option>
             <option class="py-2 px-3 text-gray-700">Female</option>
             <option class="py-2 px-3 text-gray-700">Prefer not to say</option>
        </select>
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
             Date of Birth
          </label>
          <input 
          v-model="input.date_of_birth"
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" 
          :disabled="!editable"
          type="date"
          >
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
             Civil Status
          </label>
          <select 
            v-model="input.civil_status"
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" 
            :disabled="!editable"
           label="Please select"
          >
             <!-- <option disabled value="">Please select</option> -->
             <option class="py-2 px-3 text-gray-700">Single</option>
             <option class="py-2 px-3 text-gray-700">Married</option>
             <option class="py-2 px-3 text-gray-700">Widowed</option>
             <option class="py-2 px-3 text-gray-700">Divorced</option>
          </select>
        </div>
      <div class="flex content-end">
        <button 
            v-if="editable"
            class="mr-1 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" 
            type="button"
            @click="clickSave()"
          >
          Save
        </button>
        <button 
          v-if="editable"
          class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" 
          type="button"
          @click="resetData()"
        >
          Cancel
        </button>
      </div>
    </div>

    <div v-if="!editable">
      <svg height="30" width="600" class="w-full">
        <g fill="none" stroke="grey">
          <path stroke-width="4" stroke="grey" d="M3 20 l2000 0" />
        </g>
      </svg>
      <!-- <p class="text-gray-700 pt-5">
        Activity Logs
      </p> -->
    </div>

    <div class="w-full mb-5">
      <activitylogTimeline 
      v-if="!editable"
        :activityLogData="tableData" 
      />
    </div>
<div class="mb-5 p-5"></div>
  </div>
</template>

<script>
import { mapState, mapActions, mapGetters, mapMutations } from 'vuex'
export default {
    props: {
        editable: {
            type: Boolean,
            default: true
        },
        formMethod: {
            type: String,
            default: ""
        },
    },
    data() {
        return {
            input: {
                first_name: "",
                middle_name: "",
                last_name: "",
                sex: "",
                date_of_birth: "",
                civil_status: "",
                is_active: 1,
                is_verified: 0,
                id: null,
                action: "update"
            },
            personViewDrawer: false,
            personAddDrawer: false,
            editableForm: false,
            headers: [
                {
                    name: "event",
                    sortable: true,
                    label: "Event"
                },
                {
                    name: "causer",
                    sortable: true,
                    label: "Causer"
                },
                {
                    name: "datetime",
                    sortable: true,
                    label: "Updated at"
                },
                {
                    name: "properties_formatted",
                    sortable: true,
                    label: "Properties"
                }
            ],
            // index: null,
            options: {
                page: 1,
                filters: {},
                numOfItems: 5
            }
        };
    },
    async fetch() {
        await this.updateFilterValues({}); // set the filter values to nothing every time a txn history is rendered
        await this.fetchTableData(this.options.page);
        await this.filters.forEach(filter => {
            this.getFilters({
                link: this.module,
                data: {
                    column_name: filter.field,
                    distinct: "true",
                    order_type: "ASC",
                    order_field: filter.field
                }
            });
        });
    },
    computed: {
        ...mapState({
            filterData: state => state.activitylogs.filters,
            tableData: state => state.activitylogs.data,
            pagination: state => state.activitylogs.data,
            dataLoading: state => state.activitylogs.loading,
            initialLoad: state => state.activitylogs.initialLoad,
            coursesData: state => state.activitylogs.data,
            tableFilterValues: state => state.activitylogs.filterValues,
        }),
        ...mapGetters({
            getTableData: "activitylogs/getTableData",
            getPersonByID: "persons/getDataById"
        })
    },
    methods: {
        clickSave() {
            this.$emit("onSave", this.input);
        },
        closeDrawer() {
            this.$emit("onCancel", "");
        },

        resetData() {
          const data = this.getPersonByID(this.input.id) 
          if(data){
            this.input.first_name = data.first_name;
            this.input.middle_name = data.middle_name;
            this.input.last_name = data.last_name;
            this.input.sex = data.sex;
            this.input.civil_status = data.civil_status;
            this.input.date_of_birth = data.date_of_birth;
            this.clickMakeEditable()
          }else{
            this.closeDrawer()
          }
        },
        setDefault(data) {
            this.input.id = data.id;
            this.input.first_name = data.first_name;
            this.input.middle_name = data.middle_name;
            this.input.last_name = data.last_name;
            this.input.sex = data.sex;
            this.input.civil_status = data.civil_status;
            this.input.date_of_birth = data.date_of_birth;
            this.input.is_verified = data.is_verified
            this.input.is_active = data.is_active
            this.fetchTableData(1);
        },
        clickMakeEditable() {
            this.$emit("changeEditable");
        },
        actionWithConfirmation(action){
          this.input.action = action
          this.$emit("onConfirm", action);
        },
        ...mapMutations({
            updateNumOfItems: "activitylogs/UPDATE_NUM_OF_ITEMS",
            updateFilterValues: "activitylogs/UPDATE_FILTER_VALUES",
            updateOrderValues: "activitylogs/UPDATE_ORDER_VALUES",
            setTableModule: "activitylogs/SET_MODULE"
        }),
        ...mapActions({
            getData: "activitylogs/getDataList",
            createData: "activitylogs/create",
            updateData: "activitylogs/update",
            getFilters: "activitylogs/getFilters"
        }),
        openDrawer(data) {
            this.showDrawer = true;
            this.drawerData = data;
        },
        fetchTableData(page) {
            this.getData({
                link: this.module,
                data: {
                    page,
                    // items: this.options.numOfItems,
                    subject_id: this.input.id,
                    // subject_id: '988278be-605f-4eb9-9f75-32afaf2f922f',
                    with_parent_name: true,
                    fields: [
                        "description",
                        "causer_id",
                        "updated_at",
                        "properties",
                        "event",
                        "causer"
                    ]
                }
            });
        },
        updateDrawer(index) {
            this.personViewDrawer = !this.personViewDrawer;
            if (index) {
                this.index = index.index;
            }
            else {
                this.index = null;
            }
            this.$refs.viewPerson.setDefault({
                id: index.index.id,
                description: index.index.description,
                causer_id: index.index.causer_id,
                updated_at: index.index.updated_at,
                properties: index.index.properties,
            });
            this.editableForm = false;
        },
        handleOptionsUpdate(options) {
            this.options.numOfItems = options.numOfItems;
            this.updateFilterValues(options.filters);
            this.fetchTableData(1);
        },
        handleSortingUpdate(order) {
            this.options.order_type = order.order_type;
            this.options.order_field = order.order_field;
            this.updateOrderValues(order);
            this.fetchTableData(1);
        },
        handlePagination(page) {
            this.fetchTableData(page);
        },
        async handleUpdateSave(data) {
            await this.updateData(data);
            this.personViewDrawer = await false;
            this.fetchTableData(1);
        },
        handleCancel() {
            this.personViewDrawer = false;
            this.fetchTableData(1);
        },
        async handleAddSave(data) {
            await this.createData(data);
            this.personAddDrawer = await false;
            this.fetchTableData(1);
        },
        handleAddCancel() {
            this.personAddDrawer = false;
        },
        openPersonAddDrawer() {
            this.personAddDrawer = true;
            this.$refs.addPerson.setDefault({
                id: null,
                action: "",
                by_user: "",
                action_datetime: "",
                attributes: "",
            });
        },
        handleMakeEditable() {
            this.editableForm = true;
        }
    }
}
</script>

<style>

</style>