
include ../../../makefile.inc


all: 
	$(CXX) $(COMMON_FLAGS) $(INCLUDE) -I$(ROOTPATH)/vn.lts/ltsl2 -c vnltsl2.cpp -o vnltsl2.o 
	$(CXX) $(COMMON_FLAGS) -shared -Wl,-soname,vnltsl2.so -o vnltsl2.so vnltsl2.o -L$(ROOTPATH)/vn.lts/ltsl2  $(LIBRARIES) -l:L2mduserapi.so
	cp vnltsl2.so ../test
	cp vnltsl2.so $(ROOTPATH)/vn.demo/ltsdemo
clean:
	rm *.o *.so
