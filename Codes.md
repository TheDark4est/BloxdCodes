# 昼夜变换
```
const DAY_NIGHT_CYCLE_MS = 50000*1000;
let cycleStartTime = Date.now();
const SKYBOX_DAY = {
  type:"earth",
  inclination:0,
  turbidity:5,
  luminance:1.0
};
const SKYBOX_NIGHT = {
  type:"earth",
  inclination:180,
  turbidity:15,
  luminance:0.1
};
tick = (dt) => {
  const elapsed=Date.now()-cycleStartTime, cycleProgress=(elapsed%DAY_NIGHT_CYCLE_MS)/DAY_NIGHT_CYCLE_MS;
  if(cycleProgress<0.5){setDynamicSkybox(cycleProgress*2);}else{setDynamicSkybox(1-(cycleProgress-0.5)*2);}
};
function setDynamicSkybox(darkness){const currentSkybox={type:"earth",inclination:lerp(0,180,darkness),turbidity:lerp(5,15,darkness),luminance:lerp(1.0,0.1,darkness)};
for(const playerId of api.getPlayerIds()){api.setClientOption(playerId,"skyBox",currentSkybox);}}
function lerp(start,end,t){return start+(end-start)*t;}
```
