<template>
  <div class="room border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="room-name fw-bold pe-3">{{room.name}}</div>
      <div class="room-floor text-muted pe-3">Floor : {{room.floor}}</div>
      <div class="room-currentTemp text-muted pe-3" v-if="room.currentTemp !== null">Current temperature : {{room.currentTemp}}</div>
      <div class="room-targetTemp text-muted pe-3" v-if="room.targetTemp !== null">Target Temperature : {{room.targetTemp}}</div>
      <div class="text-muted">Id : {{room.id}} </div>

      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <div class="details d-flex">
        <button type="button" class="btn btn-danger" @click="deleteRoom">Delete room</button>
      </div>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';

export default {
  name: 'RoomsListItem',
  props: ['room'],
  data: function() {
    return {
      isExpanded: false
    }
  },
  computed: {

  },
  methods: {
    toggleExpand() {
      this.isExpanded = !this.isExpanded;
    },
    async deleteRoom() {
      let response = await axios.delete(`${API_HOST}/api/rooms/${this.room.id}`);
      let roomId = this.room.id;
      this.$emit('deleted-rooms',roomId);
    }
  }
}
</script>

<style lang="scss" scoped>

.open-status {
  .icon {
    position: relative;
  }

  &.open {
    color: #198754;
    .icon {
      font-size: 12px;
      top: -3px;
    }
  }

  &.closed {
    color: #dc3545;
  }
}

.room {
  .top-row {
    cursor: pointer;
  }
}
</style>
