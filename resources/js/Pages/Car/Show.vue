<script setup>
import { Antenna, Fuel, Cog, Gauge, Car, RectangleHorizontal, MapPin, ShieldBan} from "lucide-vue-next";
import SellerInfo from "@/Views/Car/Show/SellerInfo.vue";
import ShareItem from "@/Views/Car/Show/ShareItem.vue";
import {useUtilities} from "@/Composables/useUtilities.js";

defineProps({
    car: {
        type: Object,
        required: true
    },
});

const utilities = useUtilities()
</script>

<template>
    <div class="flex flex-col space-y-4 md:space-y-10">
        <div class="flex justify-between space-x-10 ">
            <div class="w-full md:w-6/12 flex flex-col space-y-4 justify-evenly">
                <img src="../../../../public/assets/images/pl.jpg" class="rounded-lg h-56 md:h-[22rem] w-full object-cover">
                <div class="flex items-center space-x-5 min-w-full overflow-x-auto hide-scrollbar">
                    <img v-for="i in 5" src="../../../../public/assets/images/pl.jpg" :class="i === 1 ? '':'opacity-50'" class=" cursor-pointer rounded-lg h-20 min-w-28 object-cover">
                </div>
            </div>
            <div class="flex w-6/12 min-h-full space-x-6 justify-between">
                <div class="flex flex-col w-5/12 justify-between">
                    <img src="../../../../public/assets/images/pl.jpg" class="rounded-lg h-52 w-full object-cover">
                    <img src="../../../../public/assets/images/pl.jpg" class="rounded-lg h-52 w-full object-cover">
                </div>
                <img src="../../../../public/assets/images/pl.jpg" class="rounded-lg h-full md:w-7/12 object-cover">
            </div>
        </div>

        <div class="flex flex-col md:flex-row w-full justify-between">
        <div class="flex flex-col space-y-4 md:space-y-6 w-full md:bg-gray-50 md:px-5 md:pb-10 pt-5 rounded-lg md:w-6/12">
            <div class="flex justify-between items-center">
                <div class="text-3xl md:text-4xl font-semibold">{{car.car_model.car_brand.name}} {{car.car_model.name}} </div>
            </div>
            <div class="flex justify-between md:items-end md:space-x-6 items-center">
                <div class="text-xl md:text-2xl font-light border border-gray-600 px-2.5 py-0.5 rounded-lg w-fit md:bg-brand-primary md:text-white md:font-medium">{{utilities.formatNumberWithCommas(car.price)}} Br</div>
                <div class="text-sm md:font-medium md:text-base py-1 uppercase">{{car.price_type}}</div>
            </div>

            <SellerInfo :car="car" class="md:hidden"/>

            <div class="pt-3 font-semibold text-xl md:text-3xl">Overview</div>

            <div class="flex flex-col space-y-6 md:space-y-0 md:flex-row w-full md:justify-between py-2 md:text-lg">
                <div class="flex flex-col space-y-6 md:w-5/12 md:justify-evenly">
                    <div class="flex space-x-3 items-center font-medium uppercase">
                        <Antenna class="text-brand-primary"  size="15"/>
                        <div>{{car.car_condition_type.name}}</div>
                    </div>
                    <div class="flex space-x-3 items-center font-medium uppercase">
                        <Antenna class="text-brand-primary"  size="15"/>
                        <div>{{ car.transmission_type }}</div>
                    </div>
                    <div class="flex space-x-3 items-center font-medium">
                        <Gauge class="text-brand-primary"  size="16"/>
                        <div>Mileage: {{car.mileage}} Km</div>
                    </div>
                    <div class="flex space-x-3 items-center font-medium">
                        <Cog class="text-brand-primary"  size="16"/>
                        <div>Engine: {{car.engine_type.name}}</div>
                    </div>
                    <div class="flex space-x-3 items-center font-medium capitalize">
                        <Fuel class="text-brand-primary" size="16"/>
                        <div>Fuel Type: {{ car.fuel_type.name }}</div>
                    </div>

                    <div class="flex space-x-3 items-center font-medium capitalize">
                        <Car class="text-brand-primary" size="16"/>
                        <div>Body Type: {{ car.car_body_type.name }}</div>
                    </div>
                </div>
                <div class="hidden md:flex min-h-full w-0.5 bg-gray-300"></div>
                <div class="flex flex-col space-y-6 md:w-5/12 md:justify-evenly">
                    <div class="flex space-x-3 items-center font-medium">
                        <div class="w-3 h-3 rounded-full border border-gray-400" :style="'background-color:' + car.exterior_color.hex"></div>
                        <div>Exterior Color: {{ car.exterior_color.name }}</div>
                    </div>
                    <div class="flex space-x-3 items-center font-medium">
                        <div class="w-3 h-3 rounded-full border border-gray-400" :style="'background-color:' + car.interior_color.hex"></div>
                        <div>Interior Color: {{ car.interior_color.name }}</div>
                    </div>

                    <div class="flex space-x-3 items-center font-medium capitalize">
                        <RectangleHorizontal class="text-brand-primary" size="16"/>
                        <div>Plate Type: {{ car.plate_type }}</div>
                    </div>

                    <div class="flex space-x-3 items-center font-medium capitalize">
                        <MapPin class="text-brand-primary" size="16"/>
                        <div>City: {{ car.city.name }}, {{car.location}}</div>
                    </div>

                    <div class="flex space-x-3 items-center font-medium capitalize">
                        <ShieldBan class="text-brand-primary" size="16"/>
                        <div>Accident: {{ car.accident_severity }}</div>
                    </div>

                </div>
            </div>
            <ShareItem class="md:hidden"/>
        </div>
        <div class="hidden md:flex md:flex-col items-center justify-evenly w-5/12">
            <SellerInfo :car="car"/>
            <ShareItem/>
        </div>
        </div>
    </div>
</template>

<style scoped>

</style>
