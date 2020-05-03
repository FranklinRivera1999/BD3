<template>
  <div class="hello">
    <button @click="downloadExcel">DESCARGAR EXCEL</button>
  </div>
</template>

<script>
  const axios = require('axios')
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods:{
  downloadExcel(data={}){
        axios({
            url: `http://localhost:3000/api/clinicHistories/reports/allMedicine`,
            method: 'GET',
            responseType: 'blob',
            params: data
        })
        .then(response=>{
            const url= window.URL.createObjectURL(new Blob([response.data]));
            const link= document.createElement('a');
            link.href= url;
            link.setAttribute('download', 'Reporte_de_Medcinas.xlsx');
            document.body.appendChild(link);
            link.click();
        })
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

