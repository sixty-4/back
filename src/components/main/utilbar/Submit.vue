<template>
    <button @click="submit" class="uppercase p-2 text-base lg:text-xl border-2 border-slate-700 lg:mt-10 xl:mt-20 hover:bg-slate-700 hover:text-white lg:w-full">
        Submit
    </button>
</template>

<script>
import { useGenStore } from '@/store/store.js'
import { useDataStore } from '@/store/data.js'

export default {
    name: 'Submit',

    setup() {
        const genStore = useGenStore()
        const dataStore = useDataStore()

        return {
            genStore,
            dataStore,
        }
    },

    methods: {
        async submit(event) {
            event.preventDefault();

            const bodyData = {
                student: this.dataStore.studentId,
                answers: this.dataStore.pickedAns
            }

            // post method
            let headers = new Headers();
            headers.append('X-CSRFToken', `${this.genStore.token}`);
            
            const res = await fetch(`${process.env.VUE_APP_ROOT_API}/mark`, {
                method: 'POST',
                body: JSON.stringify(bodyData),
                headers: headers,
                credentials: 'include'
            })
            const data = await res.json()
            this.genStore.setSubmitTaskId(data.task);

            this.$router.replace({path: '/submited'});
        },
    },
}
</script>
