<template>
    <div id = 'view-packet'>
<ul class = "collection with-header">
    <li class = "collection-header">
        <h4> Packet Number : {{number}} </h4>
    </li>
    <li class = "collection-item">
         Time (After 1st packet) :{{time}}
    </li>
    <li class = "collection-item">
         Packet Source : {{source}}
    </li>
    <li class = "collection-item">
         Packet Protocol : {{protocol}}
    </li>
    <li class = "collection-item">
         Packet Destination : {{destination}}
    </li>
    <li class = "collection-item">
         Packet length : {{length}}
    </li>
    <li class = "collection-item">
         Packet info : {{info}}
    </li>

</ul>
<button @click = "deletePacket" class = "btn red"> Delete this Packet!!! (safe)</button>
    </div>
</template>


<script>
  import db from './firebaseInit'
  export default {
    name: 'view-packet',
    data () {
      return {
        number: null,
        time: null,
        source: null,
        protocol: null,
        destination: null,
        length: null,
        info:null

      }
    },
    beforeRouteEnter (to, from, next) {
      db.collection('packets').where('number', '==', to.params.number).get().then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          next(vm => {
            vm.number = doc.data().number
            vm.time = doc.data().time
            vm.source = doc.data().source
            vm.protocol = doc.data().protocol
            vm.destination = doc.data().destination
            vm.length = doc.data().length
            vm.info = doc.data().info


          })
        })
      })
    },
    watch: {
      '$route': 'fetchData'
    },
    methods: {
      fetchData () {
        db.collection('packets').where('number', '==', this.$route.params.number).get().then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            this.number = doc.data().number
            this.time = doc.data().time
            this.source = doc.data().source
            this.protocol = doc.data().protocol
            this.destination = doc.data().destination
            this.length = doc.data().length
            this.info = doc.data().info
          })
        })
      }
    }
  }
</script>
