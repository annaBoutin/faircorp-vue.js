<template>
 <div class="windows-list pt-3">
     <form @submit="checkForm">
        <div class="row">
           <div class="col">
             <label for="windowName">Name : </label>
		         <input id="windowName" v-model="windowName" type="Text" name="windowName" required>
	         </div>

			     <div class="col">
			        <label for="roomId">RoomID : </label>
			        <input id="roomId" v-model="roomId" type="Text" name="roomId" required>
			     </div>
	      </div>
        <br>
	      <p>
          <input type="submit" class="btn btn-primary" value="Create">
        </p>
     </form>
    <windows-list-item
      v-for="window in windows"
      :window="window"
      :key="window.id"
	  @window-updated="updateWindow"
	  @deleted-window="deleteWindow"
    >
    </windows-list-item>
  </div>
</template>


<script>
import axios from 'axios';
import {API_HOST} from '../config';
import WindowsListItem from './WindowsListItem';

export default {
  components: {
    WindowsListItem
  },
  name: 'WindowsList',
  data: function() {
    return {
      /* Initialize windows with an empty array, while waiting for actual data to be retrieved from the API */
      windows: [],
	  windowName: null,
	  roomName: null,
	  roomId: null

    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/windows`);
    let windows = response.data;
    this.windows = windows;
  },
  methods: {
    updateWindow(newWindow) {
      /* Find the place of window object with the same Id in the array, and replace it */
      let index = this.windows.findIndex(window => window.id === newWindow.id);
      this.windows.splice(index, 1, newWindow);
    },
	deleteWindow(windowId) {
      /* Delete the window of the id windowId in the array windows */
      let index = this.windows.findIndex(window => window.id === windowId);
      this.windows.splice(index,1);
    },
	checkForm(){
      const window = {"name": this.windowName, "roomName": this.roomName, "roomId": this.roomId};
      axios.post(`${API_HOST}/api/windows`, window);
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
