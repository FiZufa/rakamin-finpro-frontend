<template>
    <div class="add-room-box">
        <h1 class="title">Rent a New Room</h1>
        <form @submit.prevent="handleSubmit" class="form-body">
            <!-- Location -->
            <div class="location">
                <p>Where is the room located?</p>
                <div class="options">
                    <button
                        v-for="city in cities"
                        :key="city"
                        @click.prevent="selectLocation(city)"
                        :class="{ selected: location === city }"
                    >
                        {{ city }}
                    </button>
                </div>
                <span v-if="errors.location" class="error">{{ errors.location }}</span>
            </div>

            <!-- Room Type -->
            <div class="room-type">
                <p>Is the room <b>private</b> or <b>shared</b>?</p>
                <div class="options">
                    <button
                        v-for="type in roomTypes"
                        :key="type"
                        @click.prevent="selectRoomType(type)"
                        :class="{ selected: roomType === type }"
                    >
                        {{ type }}
                    </button>
                </div>
                <span v-if="errors.roomType" class="error">{{ errors.roomType }}</span>
            </div>

            <!-- Maximum People -->
            <div class="max-ppl">
                <p>How many beds are in the room?</p>
                <input
                    type="number"
                    v-model="beds"
                    min="1"
                    max="10"
                    placeholder="Enter the number of beds"
                />
                <span v-if="errors.beds" class="error">{{ errors.beds }}</span>
            </div>

            <!-- Superhost -->
            <div class="superhost">
                <p>Is the host a <b>superhost</b>?</p>
                <button
                    v-for="host in superhosts"
                    :key="host"
                    @click.prevent="selectHost(host)"
                    :class="{ selected: superhost === host }"
                >
                    {{ host }}
                </button>
            </div>

            <!-- Multiple Room -->
            <div class="multi">
                <p>Is this a <b>multiple</b> room?</p>
                <button
                    v-for="multi in multiples"
                    :key="multi"
                    @click.prevent="selectMulti(multi)"
                    :class="{ selected: multiple === multi }"
                >
                    {{ multi }}
                </button>
            </div>

            <!-- Business Room -->
            <div class="biz">
                <p>Is the room for <b>business</b>?</p>
                <button
                    v-for="biz in businessOptions"
                    :key="biz"
                    @click.prevent="selectBusiness(biz)"
                    :class="{ selected: business === biz }"
                >
                    {{ biz }}
                </button>
            </div>

            <!-- Distance from City Center -->
            <div class="city-center">
                <p>How far is it from the city center?</p>
                <input
                    type="number"
                    v-model="cityDistance"
                    min="1"
                    max="10"
                    placeholder="Enter distance in km"
                />
                <span v-if="errors.cityDistance" class="error">{{ errors.cityDistance }}</span>
            </div>

            <!-- Tourist Attraction Rate -->
            <div class="attr">
                <p>How would you rate the proximity to tourist attractions? (1-10)</p>
                <input
                    type="number"
                    v-model="attractionRate"
                    min="1"
                    max="10"
                    placeholder="Enter a rating"
                />
            </div>

            <!-- Proximity to Restaurants -->
            <div class="rest">
                <p>How would you rate the proximity to restaurants? (1-10)</p>
                <input
                    type="number"
                    v-model="restaurantProximity"
                    min="1"
                    max="10"
                    placeholder="Enter a rating"
                />
            </div>

            <!-- Coordinates -->
            <div class="coordinate">
                <p>Please specify the coordinates:</p>
                <div class="lat-sec">
                    <p>Latitude:</p>
                    <input
                        type="number"
                        step="0.0001"
                        v-model="latitude"
                        placeholder="Enter latitude"
                    />
                </div>
                <div class="lng-sec">
                    <p>Longitude:</p>
                    <input
                        type="number"
                        step="0.0001"
                        v-model="longitude"
                        placeholder="Enter longitude"
                    />
                </div>
            </div>

            <!-- Weekend Availability -->
            <div class="weekend">
                <p>Is the room available on the <b>weekend</b>?</p>
                <button
                    v-for="week in weekendOptions"
                    :key="week"
                    @click.prevent="selectWeekend(week)"
                    :class="{ selected: weekend === week }"
                >
                    {{ week }}
                </button>
            </div>

            <!-- Submit Button -->
            <button type="submit" class="submit-btn">Submit Room Details</button>

            <!-- Prediction Output -->
            <!-- <div v-if="prediction !== null" class="prediction-box">
                <p>Estimated Price: <b>{{ prediction }}</b></p>
            </div> -->
                <!-- Prediction Popup -->
            <PredictBox 
                v-if="showPopup" 
                :predicted_price="prediction"
                @close="showPopup = false" 
            />
        </form>
    </div>
</template>

<script>
import axios from "axios";
import PredictBox from "./PredictBox.vue";

export default {
    data() {
        return {
            location: null,
            roomType: null,
            beds: '',
            cityDistance: '',
            attractionRate: '',
            restaurantProximity: '',
            latitude: '',
            longitude: '',
            superhost: null,
            multiple: null,
            business: null,
            weekend: null,
            errors: {},
            prediction: null,
            cities: ['Athens', 'Berlin', 'Barcelona', 'Budapest', 'Lisbon', 'London', 'Paris', 'Rome', 'Vienna'],
            roomTypes: ['Private', 'Shared'],
            superhosts: ['Yes', 'No'],
            multiples: ['Yes', 'No'],
            businessOptions: ['Yes', 'No'],
            weekendOptions: ['Yes', 'No'],
            showPopup: false
        };
    },
    methods: {
        selectLocation(city) {
            this.location = city;
        },
        selectRoomType(type) {
            this.roomType = type;
        },
        selectHost(host) {
            this.superhost = host;
        },
        selectMulti(multi) {
            this.multiple = multi;
        },
        selectBusiness(biz) {
            this.business = biz;
        },
        selectWeekend(week) {
            this.weekend = week;
        },
        validateForm() {
            this.errors = {};
            if (!this.location) this.errors.location = 'Please select a location.';
            if (!this.roomType) this.errors.roomType = 'Please select a room type.';
            if (!this.beds || this.beds <= 0)
                this.errors.beds = 'Please enter a valid number of beds.';
            if (!this.attractionRate || this.attractionRate < 1 || this.attractionRate > 10)
                this.errors.attractionRate = 'Please rate proximity to attractions between 1 and 10.';
            if (!this.restaurantProximity || this.restaurantProximity < 1 || this.restaurantProximity > 10)
                this.errors.restaurantProximity = 'Please rate proximity to restaurants between 1 and 10.';
            if (!this.latitude || !this.longitude)
                this.errors.coordinates = 'Please provide valid latitude and longitude.';
            if (!this.cityDistance)
                this.errors.cityDistance = 'Please provide distance in km.';
            return Object.keys(this.errors).length === 0;
        },
        computed: {
            roomTypePrivate() {
                return this.roomType === 'Private' ? 1 : 0;
            },
            roomTypeShared() {
                return this.roomType === 'Shared' ? 1 : 0;
            }
        },
        handleSubmit() {
            if (this.validateForm()) {
                const payload = {
                    room_shared: this.roomType === 'Shared' ? 1 : 0,
                    room_private: this.roomType === 'Private' ? 1 : 0,
                    person_capacity: parseInt(this.beds),
                    host_is_superhost: this.superhost === 'Yes' ? 1 : 0,
                    multi: this.multiple === 'Yes' ? 1 : 0,
                    biz: this.buss === 'Yes' ? 1 : 0,
                    bedrooms: parseInt(this.beds),  // Assuming 'bedrooms' is the same as beds
                    dist: parseFloat(this.cityDistance),
                    metro_dist: parseFloat(this.cityDistance), // If metro_dist is different, update accordingly
                    attr_index_norm: parseFloat(this.attractionRate),
                    rest_index_norm: parseFloat(this.restaurantProximity),
                    lng: parseFloat(this.longitude),
                    lat: parseFloat(this.latitude),
                    is_weekend: this.weekend === 'Yes' ? 1 : 0,
                    room_type_Private_room: this.roomType === 'Private' ? 1 : 0,
                    room_type_Shared_room: this.roomType === 'Shared' ? 1 : 0,
                    city_Athens: this.location === 'Athens' ? 1 : 0,
                    city_Barcelona: this.location === 'Barcelona' ? 1 : 0,
                    city_Berlin: this.location === 'Berlin' ? 1 : 0,
                    city_Budapest: this.location === 'Budapest' ? 1 : 0,
                    city_Lisbon: this.location === 'Lisbon' ? 1 : 0,
                    city_London: this.location === 'London' ? 1 : 0,
                    city_Paris: this.location === 'Paris' ? 1 : 0,
                    city_Rome: this.location === 'Rome' ? 1 : 0,
                    city_Vienna: this.location === 'Vienna' ? 1 : 0,
                };

                console.log("Sending payload:", payload);

                axios.post("http://127.0.0.1:8000/predict", payload)
                    .then(response => {
                        console.log("Prediction response:", response.data);
                        // alert(`Predicted price: ${response.data.prediction}`);
                        this.prediction = response.data.prediction;
                        this.showPopup = true; // Show the popup after prediction is received
                    })
                    .catch(error => {
                        console.error("Error making prediction:", error);
                    });
            }
        },
        

    }
};
</script>

<style>
.add-room-box {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 10px;
    background: #fff;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.title {
    font-size: 24px;
    margin-bottom: 20px;
    text-align: center;
    color: #333;
}

.form-body {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.options {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
}

button {
    padding: 10px 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
    background: #f9f9f9;
    cursor: pointer;
}

button:hover {
    background: #e6e6e6;
}

button.selected {
    background: #FF385C;
    color: white;
    border-color: #FF385C;
}

input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
}

input:focus {
    border-color: #FF385C;
    outline: none;
}

.error {
    color: red;
    font-size: 12px;
}

.submit-btn {
    background: #FF385C;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
}

.submit-btn:hover {
    background: #EF2045;
}
</style>
