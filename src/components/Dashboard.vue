
<template>
    <div id = "dashboard">
<ul class="collection with-header">
    <li class =
     "collection-header">
    <h4>My Current flagged packets</h4> </li>
    
    <li v-for="packet in packets"
        v-bind:key="packet.id"
        class = "collection-item">
       
       <div class = "chip"> {{packet.number}}</div> </br>
           Packet Protocol : {{packet.protocol}} </br>
            Time (after first packet) : {{packet.time}}

   <router-link class="secondary-content" 
   v-bind:to="{ name: 'view-packet', 
   params: {number: packet.number }}">
   <i class="fa fa-eye">
       </i>
       </router-link>
   
    </li>
 </ul>   
   
   
   <div class = "fixed-action-btn">

<router-link to = "/new" 
class = "btn-floating
btn-large green"> New
<i class="fa fa-arrow"></i>
</router-link>
   </div>
    </div>
</template>


<script>
import db from './firebaseInit'
export default {
    name: 'dashboard',
    data () {
        return {
           packets: []

        }
    },
    created () {
db.collection('packets').get().then
(querySnapshot => {
    querySnapshot.forEach(doc => {
       const data = {
            'id' : doc.id,
            'number': doc.data().number,
            'time':doc.data().time,
            'source': doc.data().source,
            'protocol': doc.data().protocol,
            'destination' : doc.data().destination,
            'info' : doc.data().info,
            'length' : doc.data().length


    }
    this.packets.push(data)
    })
})   
}
}
</script>
