<template>
    <Logo/>
        
    <div class="bg-[#facea2] w-full grid px-6 sm:px-14 lg:px-0">    
        <div class="w-4/5 mx-5 my-4">
            <div class="bg-[#facea2] flex justify-end">
                <router-link to="/expln" class="hover:bg-brown3 shadow-2xl inline-block text-dark1 hover:text-white px-1 py-1 rounded-lg tracking-wider font-semibold text-sm text-white hover:shadow-lg sm:text-base">
                    <span class="font-semibold text-xs border-r-2 hover:border-r-0 pr-1 border-red-700">format for Test File</span>
                </router-link>
            </div>
            <form method="post" class="flex flex-col w-full space-y-4 justify-items-center">
                <h3 class="flex text-sm font-semibold lg:text-base">Set New Test</h3>
                <div class="lg:flex">
                    <span class="my-4 text-lg lg:text-xl lg:w-1/6">Test File</span>
                    <label class="flex w-full lg:w-3/4" for="test_file">
                        <input type="file" id="test_file" name="exam_file" accept=".txt" class="hidden lg:h-14 h-9">
                        <div class="rounded-bl-md text-md lg:text-xl inline-block py-1 lg:py-3 align-middle text-center rounded-sm w-3/5 bg-white h-9 lg:h-12" id="fileName"></div>
                        <div class="text-clip overflow-hidden rounded-br-md text-md lg:text-xl border-1 border-dark1 inline-block py-1 lg:py-3 align-middle text-center hover:outline rounded-sm w-2/5 bg-gray-400 h-9 lg:h-12">Select File</div>
                    </label>
                </div>
                <div class="lg:flex">
                    <label class="my-4 text-lg lg:text-xl lg:w-1/6" for="test_name">Title</label>
                    <input type="text" id="test_name" name="exam_name" class="hover:outline text-lg lg:text-2xl h-8 lg:h-10 border-1 border-dark1 rounded-sm w-full lg:w-3/4">
                </div>
                <div class="lg:flex">
                    <label class="my-4 text-lg lg:text-xl lg:w-1/6" for="test_date">Date</label>
                    <input type="date" id="test_date" name="exam_date" class="appearance-none hover:outline text-lg lg:text-2xl h-8 lg:h-10 border-1 border-dark1 rounded-sm w-full lg:w-3/4">
                </div>
                <div class="lg:flex">
                    <label class="my-4 text-lg lg:text-xl lg:w-1/6" for="exam_start_time">Start Time</label>
                    <input type="time" id="exam_start_time" name="exam_start_time" class="appearance-none hover:outline text-lg lg:text-2xl h-8 lg:h-10 border-1 border-dark1 rounded-sm w-full lg:w-3/4">
                </div>
                <div class="lg:flex">
                    <label class="my-4 text-lg lg:text-xl lg:w-1/6" for="exam_dur">Duration Hours</label>
                    <input placeholder="Total Hours" type="text" id="exam_dur_hr" name="exam_dur" class="hover:outline text-lg lg:text-2xl h-8 lg:h-10 border-1 border-dark1 rounded-sm w-full lg:w-3/4">
                </div>
                <div class="lg:flex">
                    <label class="my-4 text-lg lg:text-xl lg:w-1/6" for="exam_dur">Duration Minutes</label>
                    <input placeholder="Remaining Minutes" type="text" id="exam_dur_mins" name="exam_dur" class="hover:outline text-lg lg:text-2xl h-8 lg:h-10 border-1 border-dark1 rounded-sm w-full lg:w-3/4">
                </div>
                <div class="lg:flex">
                    <label class="my-4 text-lg lg:text-xl lg:w-1/6" for="test_instructions">Instructions</label>
                    <input type="text" id="test_instructions" name="test_instructions" class="hover:outline text-lg lg:text-2xl h-8 lg:h-10 border-1 border-dark1 rounded-sm w-full lg:w-3/4">
                </div>
                <div class="flex flex-row-reverse mt-6 lg:mt-0 sm:mt-8 lg:w-11/12">
                    <input @click="submitNewTest" type="submit" value="Submit" class="hover:-translate-y-0.5 bg-brown4 hover:bg-brown3 inline-block px-3 py-2 lg:px-5 lg:py-3 rounded-lg uppercase tracking-wider font-semibold text-sm text-white shadow-lg sm:text-base">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Logo from '@/components/header/Logo.vue';
import { useGenStore } from '@/store/store';
import { useCookies } from "vue3-cookies";

export default {
    name: 'NewTest',

    components: {
        Logo,
    },

    setup() {
        const genStore = useGenStore();
        const { cookies } = useCookies();
        
        return {
            genStore,
            cookies
        };
    },

    mounted() {
        this.fileChange();
    },

    methods: {
        checkFields(testDurHr, testDurMins, testDate, testStartTime, testName) {
            if (!document.querySelector("input[type=file]").files[0]) {
                alert("Please enter a File for  processing");
                return false;
            }
            else if (testName.length <= 0) {
                alert("A Test Name must be set");
                return false;
            }
            else if (testDurHr === 0 && testDurMins === 0) {
                alert("A Duration must be set");
                return false;
            }
            else if (testDate.length <= 0) {
                alert("A Test Date must be set");
                return false;
            }
            else if (testStartTime.length <= 0) {
                alert("A Test Start Time must be set");
                return false;
            }
            return true;
        },

        async submitNewTest(event) {
            event.preventDefault();
            
            //get value of all inputs
            let file = document.querySelector("input[type=file]").files[0];
            let testName = document.getElementById("test_name").value;
            let testDurHr = document.getElementById("exam_dur_hr").value.length > 0 ? document.getElementById("exam_dur_hr").value : 0;
            let testDurMins = document.getElementById("exam_dur_mins").value.length > 0 ? document.getElementById("exam_dur_mins").value : 0;;
            let testInstructions = document.getElementById("test_instructions").value;
            let testDate = document.getElementById("test_date").value;
            let testStartTime = document.getElementById("exam_start_time").value;

            if (!this.checkFields(testDurHr, testDurMins, testDate, testStartTime, testName)) {
                return;
            }

            //put all into formdata
            let formData = new FormData();
            formData.append('test_name', testName);
            formData.append('exam', file);
            formData.append('test_instructions', testInstructions);
            formData.append('hours', testDurHr);
            formData.append('minutes', testDurMins);
            formData.append('time', testDate.slice(2).split("-").reverse().join(':') + ':' + testStartTime);

            let headers = new Headers();
            headers.append('X-CSRFToken', `${this.genStore.token}`);
            // post method
            const res = await fetch(`${process.env.VUE_APP_ROOT_API}/exam/setup`, {
                method: 'POST',
                body: formData,
                headers: headers,
                credentials: 'include'
            })
            const data = await res.json();

            if (data.error) {
                alert('Some input might be missing');
                return;
            }

            document.querySelector("input[type=file]").value = null;
            document.getElementById("test_name").value = null;
            document.getElementById("exam_dur_hr").value = null;
            document.getElementById("exam_dur_mins").value = null;
            document.getElementById("test_instructions").value = null;
            document.getElementById("test_date").value = null;
            document.getElementById("exam_start_time").value = null;

            formData.delete('test_name');
            formData.delete('exam');
            formData.delete('test_instructions');
            formData.delete('hours');
            formData.delete('minutes');
            formData.delete('time');

            this.genStore.setNewTest(data);
            this.$router.push({path: '/new/test'});
        },

        fileChange() {
            let input = document.getElementById("test_file");
            let fileName = document.getElementById("fileName");

            input.addEventListener("change", ()=>{
                let inputFile = document.querySelector("input[type=file]").files[0];

                fileName.innerText = inputFile.name;
            })
        },
    },
}
</script>
