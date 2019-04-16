<template>
  <div class="hello">
    <diagram :model="model"></diagram>
  </div>
</template>

<script>
import Diagram from "./Diagram";

export default {
  data() {
    const diagramModel = new Diagram.Model();
    //diagramModel.width();
    console.log(diagramModel);
    const node1 = diagramModel.addNode("RNC_77_99", 30, 20, 250, 580);
    const outPort1 = node1.addOutPort("Port 1");
    const outPort2 = node1.addOutPort("Port 2");
    node1.color = "#66B2FF";

    const node2 = diagramModel.addNode("SR #1", 500, 20);
    const node2InPort = node2.addInPort("Gi 0/1");

    const node3 = diagramModel.addNode("SR #2", 500, 350);
    const node3InPort = node3.addInPort("Gi 0/2");
    //node4.color = "red";

    diagramModel.addLink(outPort1, node2InPort);
    diagramModel.addLink(outPort2, node3InPort);

    return {
      model: diagramModel
    };
  },

  components: {
    Diagram
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
