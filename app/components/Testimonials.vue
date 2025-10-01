<template>
    <div style="display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:16px; margin-top:18px;">
      <div class="testimonial" v-for="(t,i) in testimonials" :key="i">
        <p>"{{ t.quote }}"</p>
        <div style="margin-top:8px; font-weight:600;">{{ t.author }}</div>
      </div>
    </div>
  </template>
  
  <script setup>
  const testimonials = [
    { quote: 'slkvnslvkjskjdvbshjsb kjsb  jk dcL SDNSJK CS  JIS VK V xkc jksv sj v s jv s  bsiudvsidvbosidv  skjv bsjkv sbv vskjdbvs vjv js vjsdvubsv v jb vs vs v bsoivsvsj vj', author: 'Julio Gorge - Staff DevOps Engineer, AMD' },
    { quote: 'kjsdcnsc ns cjis cjs cs s s sj s jksbvcdsflkc acajkcajbpiasou fphsofnc sifojfcksjnsc sijhcslnc scnjfosfn snshfsihfshoifkhgisgbvm niosvbnsvncy casbcsof', author: 'Christoph Shwantze - Manager, Deloitte Consulting GmbH' },
    { quote: 'Gskcbkss shicb s chdc shc s c hjs cs  csksc sf sa fnafsaf sfsfsdfscs sdc sc ms cscs c kjs cs', author: 'Bernd Tieke - Senior IT Consultant, Sneo GmbH' },
    { quote: 'kjdsfhs jkafbda csvs cjsc sjcs sjc sc s cs cjsbc svksfjbsfj  udf ksjc jsk vcvcjk', author: 'Oluwatobi Olabiyi - AI Director, Nvidia US' }
  ]
  </script>
  