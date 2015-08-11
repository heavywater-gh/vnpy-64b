
include ../../../makefile.inc


all: 
	$(CXX) $(COMMON_FLAGS) $(INCLUDE) -I$(ROOTPATH)/vn.lts/ltsapi -c vnltstd.cpp -o vnltstd.o 
	$(CXX) $(COMMON_FLAGS) -shared -Wl,-soname,vnltstd.so -o vnltstd.so vnltstd.o -L$(ROOTPATH)/vn.lts/ltsapi  $(LIBRARIES) -l:securitymduserapi.so -l:securitytraderapi.so
	cp vnltstd.so ../test
	cp vnltstd.so $(ROOTPATH)/vn.demo/ltsdemo
clean:
	rm *.o *.so
