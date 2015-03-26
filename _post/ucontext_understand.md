## ucontext 接口理解 ##
 - getcontext(struct ucontext_t*)
 初始化struct ucontext_t结构体，且默认记录当前上下文作为调用setcontext时恢复的入口点
 - setcontext(const struct ucontext_t*)
 根据传入 struct ucontext_t结构体，跳转到指定入口点，且该接口调用处的上下文不可恢复
 - makecontext(struct ucontext_t*, func, int, ...)
 设置指定函数以及参数列表作为struct ucontext_t上下文的入口点
 - swapcontext(struct ucontext_t* a, struct ucontext_t* b)
 记录当前上下文到a，并切换到上下文b，在执行后可通过反向swapcontext(b, a); 且还回节点
