<template>
 <div class="m-4 p-5 shadow-xl rounded-lg border-blue-300 border-2 overflow-hidden">
  <div class="lg:flex lg:items-center lg:justify-between">
    <div class="flex-1 min-w-0">
        <h2 class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate">
        {{event.name}}
        </h2>
        <div class="mt-1 flex flex-col sm:flex-row sm:flex-wrap sm:mt-0 sm:space-x-6">
        <div class="mt-2 flex items-center text-sm text-gray-500">
            <!-- Heroicon name: briefcase -->
            <i class="fas fa-chair mx-2"></i>
            Seats: {{event.seats.length}}
        </div>
        <div class="mt-2 flex items-center text-sm text-gray-500">
            <!-- Heroicon name: location-marker -->
            <i class="fas fa-chair mx-2"></i>
            Seats Sold: {{seatsUnavailable.length}}
        </div>
        <div class="mt-2 flex items-center text-sm text-gray-500">
            <!-- Heroicon name: calendar -->
            <i class="far fa-calendar-check mx-2"></i>
            {{event.date}}
        </div>
        <div class="mt-2 flex items-center text-sm text-gray-500">
            <!-- Heroicon name: calendar -->
            <i class="fas fa-door-open mx-2"></i>
            <span v-if="event.access == 1">Open</span>
            <span v-if="event.access == 0">Closed</span>
        </div>
        </div>
    </div>
    <div class="mt-5 flex lg:mt-0 lg:ml-4">

        <span class="sm:ml-3">
        <button @click="$emit('del-event', event.id)" type="button" class="inline-flex items-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            <!-- Heroicon name: check -->
            <i class="fas fa-trash -ml-1 mr-2"></i>
            Delete
        </button>
        </span>
    </div>
  </div>
 </div>
</template>

<script>
export default {
    name: "EventManagerItem",
    props: ["event"],
    data(){
        return{
            seatsUnavailable: []
        }
    },
    created(){
        for(var i = 0; i < this.event.seats.length; i++){
            if(this.event.seats[i].available == false){
                this.seatsUnavailable.push(this.event.seats[i]);
            }
        }
    }

}
</script>