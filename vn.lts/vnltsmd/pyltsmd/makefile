
include ../../../makefile.inc


all: 
	$(CXX) $(COMMON_FLAGS) $(INCLUDE) -I$(ROOTPATH)/vn.lts/ltsapi -c vnltsmd.cpp -o vnltsmd.o 
	$(CXX) $(COMMON_FLAGS) -shared -Wl,-soname,vnltsmd.so -o vnltsmd.so vnltsmd.o -L$(ROOTPATH)/vn.lts/ltsapi  $(LIBRARIES) -l:securitymduserapi.so -l:securitytraderapi.so
	cp vnltsmd.so ../test
	cp vnltsmd.so $(ROOTPATH)/vn.demo/ltsdemo
clean:
	rm *.o *.so
