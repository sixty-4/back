<template>
    <Logo/>
    <div class="bg-[#facea2] grid px-6 sm:px-14 lg:px-0">
        <div class="mb-3 lg:ml-6 lg:w-5/6">
            <h2 class="text-lg font-semibold font1 mb-4 mt-6 text-lg lg:text-xl">How to format the ".txt" file to include all of the question's details</h2>
            <div class="text-center">
                <div class="font2 px-5">
                    <p class="text-left italic md:text-lg">
                        <span class="text-left">
                            { <br>
                            <b>%N</b> Q (The number should be separated by space or a character from the question)<br>
                            <b>%O</b> o (max of 4) <br>
                            <b>answer=</b>A <br>
                            }
                        </span> <br>
                        <br>
                        where <b>N</b> is number of question <br>
                        where <b>O</b> is option identifier (max of 4, <span class="underline font-medium">must be alphabet</span>) <br>
                        where <b>answer=</b> is answer identifier <br>
                        where <b>Q</b> is question <br>
                        where <b>o</b> is option <br>
                        where <b>A</b> is the answer <br>
                    </p>
                    <br>
                    <p class="bg-white px-3 text-left text-md md:text-xl">
                        <b><span class="uppercase">example</span></b> <br>
                        <u>%1</u> A small handcart, one wheel and tire shafts used for moving farm crop material is ? <br>
                        <u>%a</u> cup <u>%b</u> wheelbarrow <u>%c</u> kettle  <br>
                        <u>answer=</u>wheelbarrow <br>
                        . . . <br>
                        <u>%14</u> Weeds are ? <br>
                        <u>%a</u> planted plants <u>%b</u> timber tree <u>%c</u> unwanted plants <br>
                        <u>answer=</u>unwanted plants <br>
                        . . .
                    </p>
                </div>
            </div>
        </div>
        <div class="mb-4 flex justify-center">
            <router-link  to="/set_test" class="hover:bg-brown4 inline-block px-5 py-3 rounded-lg bg-brown3 uppercase tracking-wider font-semibold text-sm text-white shadow-lg sm:text-base">
                Set Test
            </router-link>
        </div>
    </div>
</template>

<script>
import Logo from '@/components/header/Logo.vue';

export default {
    name: 'Expln',

    components: {
        Logo,
    },
}
</script>
