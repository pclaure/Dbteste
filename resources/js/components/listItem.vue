<template>

    <tbody>
        <tr>
            <th scope="row">{{ task.id }}</th>
            <td>{{ task.nome }}</td>
            <td>{{ task.descricao }}</td>
            <td>{{ getStatus(task.status) }}</td>
            <td>
                <button class="btn btn-primary ml-3" :disabled="isDisabledPegar(task)" @click="updateCheck(task, 2)"><i class="fa fa-handshake-o" aria-hidden="true"></i></button>
                <button class="btn btn-success ml-3" :disabled="isDisabledFinaliza(task)" @click="updateCheck(task, 3)">&check;</button>
                <button class="btn btn-success ml-3" @click="showModal = true"><i class="fa fa-plus-square-o" aria-hidden="true"></i></button>

            </td>
            
        </tr>
    </tbody> 
       
       
</template>

<script>
export default {
    props: ["task"],
    
    methods: {
        showModal() {
            this.isModalVisible = true;
        },
        isDisabledPegar(task) {
        // you can  check your form is filled or not here.
        if(task.status==1)
            return false;
        else
            return true;
      },
      isDisabledFinaliza(task) {
        // you can  check your form is filled or not here.
        if(task.status==2)
            return false;
        else
            return true;
      },
        getStatus(id){
            var ret = "";
            switch (id) {
                case "1":
                ret =  "Aberta";
                    break;
                case "2":
                ret =  "Em andamento";
                    break;
                case "3":
                ret =  "Finalizada";
                    break;
                default:
                ret =  "Aberta";
                    break;
            }
            return ret;
        },
        updateCheck(task, status) {
            task.status = status;
            axios
                .put(`api/task/${task.id}`, {
                    item: task
                })
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios put", errors);
                });
        },
        removeItem() {
            axios
                .delete(`api/task/${this.item.id}`)
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios delte ", error);
                });
        }
    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: gray;
}
.item {
    word-break: break-all;
}
</style>
