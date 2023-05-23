<template>
  <div py4>
    <div grid="~ cols-3 rows-3 gap-10" text-center items-center justify-center h-full class="group">
      <a href="#" class="box !hover:text-violet">
        <div font-mono op80 text-sm>01. 条件 </div>
        <div text-sm op60>T extends U ? X : Y</div>
      </a>
      <a href="#" class="box !hover:text-rose">
        <div font-mono op80 text-sm>02. 约束 </div>
        <div text-sm op60>extends</div>
      </a>
      <a href="#" class="box !hover:text-amber">
        <div font-mono op80 text-sm>03. 推导 </div>
        <div text-sm op60>infer </div>
      </a>
      <a href="#" class="box !hover:text-green">
        <div font-mono op80 text-sm>04. 联合 </div>
        <div text-sm op60> | </div>
      </a>
      <a href="#" class="box !hover:text-red">
        <div font-mono op80 text-sm>05. 交叉 </div>
        <div text-sm op60> & </div>
      </a>
      <a href="#" class="box !hover:text-teal">
        <div font-mono op80 text-sm>06. 索引查询 </div>
        <div text-sm op60>keyof </div>
      </a>
      <a href="#" class="box !hover:text-pink">
        <div font-mono op80 text-sm>07. 索引访问 </div>
        <div text-sm op60>T[K] </div>
      </a>
      <a href="#" class="box !hover:text-yellow">
        <div font-mono op80 text-sm>08. 索引遍历 </div>
        <div text-sm op60>in </div>
      </a>
      <a href="#" class="box !hover:text-purple">
        <div font-mono op80 text-sm>09. 重映射 </div>
        <div text-sm op60>as </div>
      </a>
    </div>
  </div>
</template>

<style scoped>
.box {
  --at-apply: 'flex items-center gap-4 px2 py4 rounded-5px transition-all duration-600 rounded !hover:op100 group-hover:op50';

  border: 1px solid #4b5162;
}

.box:hover {
  box-shadow: 0 0 10px #4b5162;
}
</style>
