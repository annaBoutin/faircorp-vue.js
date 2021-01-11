<template>
  <div class="rooms-list pt-3">
    <form @submit="checkForm">
      <div class="row">
        <div class="col">
          <label for="roomName">Name : </label>
          <input id="roomName" v-model="roomName" type="Text" name="roomName" required>
        </div>
        <div class="col">
          <label for="roomFloor">Floor : </label>
          <input id="roomFloor" v-model="roomFloor" type="Number" name="roomFloor" required min="0">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="roomCurrentTemp">Current Temperature : </label>
          <input id="roomCurrentTemp" v-model="roomCurrentTemp" type="number" CurrentTemp="roomCurrentTemp">
        </div>
        <div class="col">
          <label for="roomTargetTemp">Target Temperature : </label>
          <input id="roomTargetTemp" v-model="roomTargetTemp" type="number" TargetTemp="roomTargetTemp">
        </div>
      </div>
      <br>
      <p>
        <input type="submit" class="btn btn-primary" value="Create">
      </p>
    </form>
    <rooms-list-item
      v-for="room in rooms"
      :room="room"
      :key="room.id"
      @deleted-room="deleteRoom"
    >
    </rooms-list-item>
  </div>
</template>


<script>
import axios from 'axios';
import {API_HOST} from '../config';
import RoomsListItem from './RoomsListItem';

export default {
  components: {
    RoomsListItem
  },
  name: 'RoomsList',
  data: function() {
    return {
      /* Initialize windows with an empty array, while waiting for actual data to be retrieved from the API */
      rooms: [],
      roomName: null,
      roomFloor: null,
      roomCurrentTemp: null,
      roomTargetTemp: null
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/rooms`);
    let rooms = response.data;
    this.rooms = rooms;
  },
  methods: {
    deleteRoom(roomId) {
      /* Delete the room of the id roomId in the array rooms */
      let index = this.rooms.findIndex(room => room.id === roomId);
      this.rooms.splice(index,1);
    },
    checkForm(){
      const room = {"name": this.roomName, "floor": this.roomFloor, "currentTemp": this.roomCurrentTemp, "targetTemp": this.roomTargetTemp};
      axios.post(`${API_HOST}/api/rooms`, room);
    }
  }
}
</script>

<style lang="scss" scoped>
.row {
    background: #ccc;
    border: 1px solid #ccc;
    overflow: hidden;
    padding: 10px;
}
.col {
    float: left;
    width: 50%
}

</style>
