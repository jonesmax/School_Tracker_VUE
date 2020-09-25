<template>
    <div id="appMain">
        <div id="main">
            <div v-if="projects && projects.length" id="assignment">
                
                <div v-for="item in projects" :key="item.id">
                    
                   <button :style="'border-color:'+findColor(item.course_id)" @click="showModal=item,info= item">{{ convertDate(item.assignment_dueDate) +" - "+item.assignment_name}}</button>     
                    

                </div>
            </div>

            <transition name = "fade" appear>
                        <div class = "modal-overlay" v-if="showModal" @click="showModal=false">
                        
                            <h2>Assignemnt ID: {{info.id}}</h2>
                            <h2>Course ID: {{info.course_id}}</h2>
                            <h2>Assignment Name: {{info.assignment_name}}</h2>
                            <h2>Notes: {{info.notes}}</h2>
                            <button  @click="removeAssignment(info.id)">Complete</button>  
                        </div>
            </transition>
         
        </div>
        <transition name = "fade" appear>
                <div class = "modal-overlay2" v-if="showModal2==true">
                    <div id = "addLine">

                        <select v-model="selected">
                            <option disabled value="">Please select one</option>
                            <option value = 1>Obj Oriented Analysis/Modeling</option>
                            <option value = 2>Data Structures & Algorithms</option>
                            <option value = 4>Advanced Databases</option>
                            <option value = 5>Client/Server Application Dev</option>
                            <option value = 6>Network Fund for Programmers</option>
                            <option value = 7>Co-op Educ. Employment Prep</option>
                            <option value = 8>Communications for IT</option>
                        </select>
                        <input v-model="project_name_feild" placeholder="Project Name">
                        <input v-model="due_date_feild" placeholder="Due Date">

                        <select v-model="priority_selected">
                            <option disabled value="">Please select one</option>
                            <option value = 1>1</option>
                            <option value = 2>2</option>
                            <option value = 3>3</option>
                            <option value = 4>4</option>
                            <option value = 5>5</option>
                            
                        </select>
                        <input v-model="note_feild" placeholder="Notes">
                    </div>   
                    <button  @click="showModal2=false,addAssignment()">Add</button>   
                    <button  @click="showModal2=false">Close</button>        
                </div>
                 
        </transition>
        <div id="buttonBottom">
            <button  @click="showModal2=true">+</button>  
        </div>

    </div>
    
</template>

<script>
    import axios from 'axios';

    export default {
        data() {
            return {
                projects: null,
                selected: '',
                project_name_feild: '',
                due_date_feild: '',
                priority_selected: '',
                courses: [],
                showModal: false,
                currentDate: null,
                counter: 0,
                showModal2: false

            }
        },
        methods:{
            convertDate(date){
                var new_date = new Date(date);
                var months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sept", "Oct", "Nov", "Dec"];
                return months[new_date.getMonth()]+" "+(new_date.getDate())
            },
            findColor(id) {
            let course = this.courses.find(course => course.id == id)
            if (course)
                return course.colour
            },
            addAssignment(){
                var payload={
                    course_id: this.selected,
                    assignment_name: this.project_name_feild,
                    assignment_dueDate: this.due_date_feild,
                    assignment_status: 0,
                    priority: this.priority_selected,
                    notes: this.note_feild
                }
                axios.post('http://3.23.114.13/assignments', payload).then(() => {
                    this.updateTable()
                })
                
            },
            removeAssignment(assignment_id){
                axios.delete('http://3.23.114.13/assignments/'+assignment_id).then(() => {
                    this.updateTable()
                })
             
            },
            updateTable(){
                axios.get('http://3.23.114.13/assignments/sorted/4')
                .then(response => {
                    this.projects = Object.values(response.data);
                    
                    
                })
                axios.get('http://3.23.114.13/courses/4')
                .then(response => {
                    this.courses = response.data;
                    console.log(response.data)
                })
            },
            addClass(){
                var payload={
                    user_id: 4,
                    course_name: "COMM-3077-41 Communications for IT",
                    prof_name: "Zeinab McHeinmech",
                    colour: "cyan"
                }
                axios.post('http://3.23.114.13/courses', payload).then(() => {
                    this.updateTable()
                })
            },
            updateCourse(){
                var payload={
                    user_id: 4,
                    course_name: "COMM-3077-41 Communications for IT",
                    prof_name: "Zeinab McHeinmech",
                    colour: "yellow",
                    id: 8
                }
                axios.put('http://3.23.114.13/courses', payload).then(() => {
                    this.updateTable()
                })
            },
            
        },
            mounted(){
                this.updateTable()


            }
    }
</script>

<style scoped>

#appMain{
    background-color: rgb(255, 255, 255,0.8)!important;
    width: 15%;
    height: 100%;
    padding: 0.77%;
    box-shadow: 8px 8px 15px rgb(66, 66, 66);
}

#assignment{
    background-color: white!important;
    
}

h2{
    
    font-size: 20px;
    color: white;
    display: block;
    padding: 1%;
}
h3{
    margin: 0;
    padding: 0.5%;
    font-size: 12px;
}
#assignment button{
    display: block;
    width:100%;
    padding: 2.05%;
    margin: 0px;
    font-size: 22px;
    color: rgb(0, 0, 0);
    border-style: none none none solid!important;
    border-width: 25px;
    /* text-shadow: 1px 2px 3px rgb(82, 82, 82); */
    font-family: 'Pragati Narrow', sans-serif;
    text-align: left;
    box-shadow: 0 0 5px rgb(175, 175, 175);
    padding-left: 4%;
}
#assignment button:hover{
    cursor: pointer;
    opacity: 80%!important;

}
#assignment button:active{
    border-style: none;

}
#addLine{
   
    padding: 3%;
    display: block;
}

.modal-overlay{
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 98;
    margin: auto;
    background-color:white;
    border-style: solid;
    width: 20%;
    height: 20%;
    padding: 2%;
    font-family: Arial, Helvetica, sans-serif;
}

.modal-overlay2 button{
    width: 60%;
    

}
.modal-overlay2{
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 98;
    margin: auto;
    background-color:white;
    border-style: solid;
    width: 20%;
    height: 20%;
    padding: 1%;
}
.modal-overlay button{
    color: black!important;
    width: 50%!important;
    border-style: solid!important;
    border-color: black!important;
    margin: auto!important;
    padding: 2%!important;
}
.modal-overlay button:hover{
    background-color: rgb(228, 227, 227);
    
}
.modal-overlay h2{
    color: black;
}
#buttonBottom button{
    display: block;
    width:100%;
    padding: 1.9%;
    margin: 0;
    font-size: 20px;
    color: rgb(0, 0, 0);
    border-style: solid none none none;
    border-color: rgb(255, 255, 255);
    /* text-shadow: 1px 2px 3px rgb(82, 82, 82); */
    box-shadow: 0 0 5px rgb(134, 134, 134);
    font-family:'Arial Narrow Bold', sans-serif;
    
}
#buttonBottom button:hover{
    background-color: rgb(255, 255, 255);
}

#app{
    border-style: inset;
    background-image: none!important;

}
@media only screen and (max-width: 2000px) {
    #assignment button{
        padding: 1.2%;
    }
    #appMain{
        width: 20%;
    }
}
</style>