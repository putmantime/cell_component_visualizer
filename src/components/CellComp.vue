<template>
  <div id="main-div"></div>
</template>
<script>
  /* eslint-disable */
  import * as d3 from 'd3';
  import axios from 'axios';

  const go_map = {
    'GO:0005794': '.golgi',
    'GO:0005768': '.endosome',
    'GO:0005777': '.peroxisome',
  };

  export default {
    name: 'CellComp',
    data() {
      return {};
    },
    props: ['goTerm'],
    methods: {
      loadSVG: function () {
        const _this = this;
        const mainDiv = d3.select('#main-div');
        d3.xml("../../static/img/chlambase_subcell.svg")
          .mimeType("image/svg+xml")
          .get(function (error, xml) {
            if (error) throw error;
            mainDiv.node().appendChild(xml.documentElement);
            const cell_comp = mainDiv.selectAll(go_map[_this.goTerm]);
            cell_comp.attr('fill', '#4784FF');
          });
      },
      get_ontology_parents: function (goTerm) {
        const _this = this;
        const url = 'https://www.ebi.ac.uk';
        const testTerm = 'GO_0020015';
        const term = goTerm.replace(':', '_');
        const endpoint = '/ols/api/ontologies/go/terms/';
        const iri = encodeURIComponent(
          encodeURIComponent(
            `http://purl.obolibrary.org/obo/${testTerm}`
          )
        );
        axios.get(url + endpoint + iri + '/hierarchicalAncestors')
          .then((resp) => {
            // eslint-disable-next-line
            const terms = resp.data._embedded.terms;
            terms.forEach(function(data){
              console.log(data);
            });
          })
          .catch((err) => {
            // eslint-disable-next-line
            console.log(err);
          });
        ;
      }
    },
    mounted() {
      this.loadSVG();
      this.get_ontology_parents(this.goTerm);
      console.log(go_map[this.goTerm]);

    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  svg {
    margin: 25px;
    pathfill: none;
    stroke: #76BF8A;
    stroke-width: 3px;
  }
</style>
