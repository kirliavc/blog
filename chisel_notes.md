
### Initializing Vectors
```
val reg=RegInit(VecInit(Seq.fill(4)(0.U(32.W))))
```

### Array Index

both chisel type and scala type can be array index(?)

### Generate Verilog

https://github.com/freechipsproject/chisel3/wiki/Frequently-Asked-Questions

### 在一个Module中，嵌入一组Module（形成一个Module的向量）
```
 val my_args = Seq(1,2,3,4)
    val exe_units = for (i <- 0 until num_units) yield {
       val exe_unit = Module(new AluExeUnit(args = my_args(i)))
       // any wiring or other logic can go here
       exe_unit
    }
   ```

### Init Reg Vector

https://github.com/freechipsproject/chisel3/wiki/Cookbook#how-do-i-create-a-reg-of-type-vec
