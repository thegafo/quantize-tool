<script>
  import { onMount } from "svelte";

  const process = (canvas) => {
    const context = canvas.getContext("2d");
    const imgData = context.getImageData(0, 0, canvas.width, canvas.height);
    const data = imgData.data;

    // enumerate all pixels
    // each pixel's r,g,b,a datum are stored in separate sequential array elements

    const pallet0 = [
      [30, 10, 10],
      [101, 93, 138],
      [216, 133, 163],
      [253, 206, 185],
    ];

    const pallet1 = [
      [10, 10, 10],
      [254, 201, 70],
      [36, 144, 233],
      [250, 171, 28],
      [18, 97, 188],
      [228, 110, 99],
      [228, 152, 136],
    ];

    const hydra = [
      [228, 96, 160],
      [25, 53, 155],
      [13, 14, 94],
      [114, 273, 220],
    ];

    const clusters = [
      [0, 129, 167],
      [0, 175, 185],
      [253, 252, 220],
      [254, 217, 183],
      [240, 113, 103],
    ];

    const mapping = clusters;

    const distance = (a, b) => {
      return (
        ((a[0] - b[0]) ** 2 + (a[1] - b[1]) ** 2 + (a[2] - b[2]) ** 2) ** 0.5
      );
    };

    for (let i = 0; i < data.length; i += 4) {
      const red = data[i];
      const green = data[i + 1];
      const blue = data[i + 2];
      const alpha = data[i + 3];
      const rgb = [red, green, blue];
      let minDistance = Number.MAX_SAFE_INTEGER;
      let minCluster = null;
      let minClusterIndex = null;
      for (let j = 0; j < mapping.length; j++) {
        const cluster = mapping[j];
        const dist = distance(cluster, rgb);
        if (dist <= minDistance) {
          minDistance = dist;
          minCluster = cluster;
          minClusterIndex = j;
        }
      }
      data[i] = mapping[minClusterIndex][0];
      data[i + 1] = mapping[minClusterIndex][1];
      data[i + 2] = mapping[minClusterIndex][2];
      data[i + 3] = alpha;
    }
    context.putImageData(imgData, 0, 0);
  };

  onMount(() => {
    console.log("mounted");
    const canvas = document.getElementById("viewport"),
      context = canvas.getContext("2d");
    const image = new Image();
    image.src = "/bg4.png";

    image.onload = () => {
      canvas.width = image.width;
      canvas.height = image.height;
      context.drawImage(image, 0, 0);
      process(canvas);
    };
  });
</script>

<canvas id="viewport" />

<style>
  canvas#viewport {
    border: 1px solid white;
  }
</style>
