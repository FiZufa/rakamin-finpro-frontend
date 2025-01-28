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
                <span v-if="errors.attractionRate" class="error">{{ errors.attractionRate }}</span>
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
                <span v-if="errors.restaurantProximity" class="error">{{ errors.restaurantProximity }}</span>
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
                <span v-if="errors.coordinates" class="error">{{ errors.coordinates }}</span>
            </div>

            <!-- Submit Button -->
            <button type="submit" class="submit-btn">Submit Room Details</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            location: null,
            roomType: null,
            beds: '',
            attractionRate: '',
            restaurantProximity: '',
            latitude: '',
            longitude: '',
            errors: {},
            cities: ['Athens', 'Berlin', 'Barcelona', 'Budapest', 'Lisbon', 'London', 'Paris', 'Rome', 'Vienna'],
            roomTypes: ['Private', 'Shared'],
        };
    },
    methods: {
        selectLocation(city) {
            this.location = city;
        },
        selectRoomType(type) {
            this.roomType = type;
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
            return Object.keys(this.errors).length === 0;
        },
        handleSubmit() {
            if (this.validateForm()) {
                alert('Form submitted successfully!');
                // Handle form data submission here
            }
        },
    },
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
