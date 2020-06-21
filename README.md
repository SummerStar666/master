# master

## 逻辑修改
在函数Conpute中，当参数小于8时，会返回除以5的余数；当参数大于等于8时，会返回当前这个整数n加上Compute(n-1)的结果。
```go
//处理数据并进行记录

func index(w http.ResponseWriter, r *http.Request) {

	timer:=metrics.NewAdmissionLatency()
	metrics.RequestIncrease()
	num:=os.Getenv("Num")

	if num==""{
		Compute(6)
		_,err:=w.Write([]byte("there is no env Num. Computation successed\n"))
		
    if err!=nil{
			log.Println("err:"+err.Error()+" No\n")
		}
	}else{
		numInt,_:=strconv.Atoi(num)
		Compute(numInt)
		_,err:=w.Write([]byte("there is env Num. Computation successed\n"))
		
    if err!=nil{
			log.Println("err:"+err.Error()+" Yes\n")
		}
	}
	timer.Observe()
}

//用于计算的函数
func Compute(n int)int{

	if n < 8{
		return n%5
	}else{
		return n + Compute(n-1)
	}
  
}
```
