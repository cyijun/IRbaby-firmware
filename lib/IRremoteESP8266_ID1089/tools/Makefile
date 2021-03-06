# SYNOPSIS:
#
#   make [all]  - makes everything.
#   make clean  - removes all files generated by make.

# Please tweak the following variable definitions as needed by your
# project, except GTEST_HEADERS, which you can use in your own targets
# but shouldn't modify.


# Where to find user code.
USER_DIR = ../src

# Where to find test code.
TEST_DIR = ../test

# Flags passed to the preprocessor.
# Set Google Test's header directory as a system directory, such that
# the compiler doesn't generate warnings in Google Test headers.
CPPFLAGS += -DUNIT_TEST

# Flags passed to the C++ compiler.
CXXFLAGS += -g -Wall -Wextra -pthread

all : gc_decode mode2_decode

run_tests : all
	failed=""; \
	for py_unittest in *_test.py; do \
	  echo "RUNNING: $${py_unittest}"; \
		python ./$${py_unittest} || failed="$${failed} $${py_unittest}"; \
	done; \
	if [ -n "$${failed}" ]; then \
		echo "FAIL: :-( :-( Unit test(s)$${failed} failed! :-( :-("; exit 1; \
	else \
		echo "PASS: \o/ \o/ All unit tests passed. \o/ \o/"; \
	fi

clean :
	rm -f  *.o *.pyc gc_decode mode2_decode


# All the IR protocol object files.
PROTOCOLS = ir_NEC.o ir_Sony.o ir_Samsung.o ir_JVC.o ir_RCMM.o ir_RC5_RC6.o \
            ir_LG.o ir_Mitsubishi.o ir_Fujitsu.o ir_Sharp.o ir_Sanyo.o \
            ir_Denon.o ir_Dish.o ir_Panasonic.o ir_Whynter.o ir_Coolix.o \
            ir_Aiwa.o ir_Sherwood.o ir_Kelvinator.o ir_Daikin.o ir_Gree.o \
            ir_Pronto.o ir_GlobalCache.o ir_Nikai.o ir_Toshiba.o ir_Midea.o \
            ir_Magiquest.o ir_Lasertag.o ir_Carrier.o ir_Haier.o ir_Hitachi.o \
            ir_GICable.o ir_Whirlpool.o ir_Lutron.o ir_Electra.o ir_Pioneer.o \
            ir_MWM.o

# Common object files
COMMON_OBJ = IRutils.o IRtimer.o IRsend.o IRrecv.o $(PROTOCOLS)

# Common dependencies
COMMON_DEPS = $(USER_DIR)/IRrecv.h $(USER_DIR)/IRsend.h $(USER_DIR)/IRtimer.h \
              $(USER_DIR)/IRutils.h $(USER_DIR)/IRremoteESP8266.h
# Common test dependencies
COMMON_TEST_DEPS = $(COMMON_DEPS) $(TEST_DIR)/IRsend_test.h

gc_decode.o : gc_decode.cpp $(COMMON_TEST_DEPS) $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -I$(USER_DIR) -I$(TEST_DIR) -c gc_decode.cpp

gc_decode : $(COMMON_OBJ) gc_decode.o
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -lpthread $^ -o $@

mode2_decode.o : mode2_decode.cpp $(COMMON_TEST_DEPS) $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -I$(USER_DIR) -I$(TEST_DIR) -c mode2_decode.cpp

mode2_decode : $(COMMON_OBJ) mode2_decode.o
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -lpthread $^ -o $@

IRutils.o : $(USER_DIR)/IRutils.cpp $(USER_DIR)/IRutils.h $(USER_DIR)/IRremoteESP8266.h
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/IRutils.cpp

IRtimer.o : $(USER_DIR)/IRtimer.cpp $(USER_DIR)/IRtimer.h
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/IRtimer.cpp

IRsend.o : $(USER_DIR)/IRsend.cpp $(USER_DIR)/IRsend.h $(USER_DIR)/IRremoteESP8266.h
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/IRsend.cpp

IRrecv.o : $(USER_DIR)/IRrecv.cpp $(USER_DIR)/IRrecv.h $(USER_DIR)/IRremoteESP8266.h $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/IRrecv.cpp


ir_NEC.o : $(USER_DIR)/ir_NEC.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_NEC.cpp

ir_GlobalCache.o : $(USER_DIR)/ir_GlobalCache.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_GlobalCache.cpp

ir_Sherwood.o : $(USER_DIR)/ir_Sherwood.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Sherwood.cpp

ir_Sony.o : $(USER_DIR)/ir_Sony.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Sony.cpp

ir_Samsung.o : $(USER_DIR)/ir_Samsung.cpp $(USER_DIR)/ir_Samsung.h $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Samsung.cpp

ir_Kelvinator.o : $(USER_DIR)/ir_Kelvinator.cpp $(USER_DIR)/ir_Kelvinator.h $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Kelvinator.cpp

ir_JVC.o : $(USER_DIR)/ir_JVC.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_JVC.cpp

ir_RCMM.o : $(USER_DIR)/ir_RCMM.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_RCMM.cpp

ir_LG.o : $(USER_DIR)/ir_LG.h $(USER_DIR)/ir_LG.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_LG.cpp

ir_Mitsubishi.o : $(USER_DIR)/ir_Mitsubishi.h $(USER_DIR)/ir_Mitsubishi.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Mitsubishi.cpp

ir_Fujitsu.o : $(USER_DIR)/ir_Fujitsu.h $(USER_DIR)/ir_Fujitsu.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Fujitsu.cpp

ir_Sharp.o : $(USER_DIR)/ir_Sharp.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Sharp.cpp

ir_RC5_RC6.o : $(USER_DIR)/ir_RC5_RC6.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_RC5_RC6.cpp

ir_Panasonic.o : $(USER_DIR)/ir_Panasonic.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Panasonic.cpp

ir_Dish.o : $(USER_DIR)/ir_Dish.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Dish.cpp

ir_Whynter.o : $(USER_DIR)/ir_Whynter.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Whynter.cpp

ir_Coolix.o : $(USER_DIR)/ir_Coolix.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Coolix.cpp

ir_Aiwa.o : $(USER_DIR)/ir_Aiwa.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Aiwa.cpp

ir_Denon.o : $(USER_DIR)/ir_Denon.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Denon.cpp

ir_Sanyo.o : $(USER_DIR)/ir_Sanyo.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Sanyo.cpp

ir_Daikin.o : $(USER_DIR)/ir_Daikin.cpp $(USER_DIR)/ir_Daikin.h $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Daikin.cpp

ir_Gree.o : $(USER_DIR)/ir_Gree.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Gree.cpp

ir_Pronto.o : $(USER_DIR)/ir_Pronto.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Pronto.cpp

ir_Nikai.o : $(USER_DIR)/ir_Nikai.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Nikai.cpp

ir_Toshiba.o : $(USER_DIR)/ir_Toshiba.h $(USER_DIR)/ir_Toshiba.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Toshiba.cpp

ir_Midea.o : $(USER_DIR)/ir_Midea.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Midea.cpp

ir_Magiquest.o : $(USER_DIR)/ir_Magiquest.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Magiquest.cpp

ir_Lasertag.o : $(USER_DIR)/ir_Lasertag.cpp $(USER_DIR)/ir_RC5_RC6.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Lasertag.cpp

ir_Carrier.o : $(USER_DIR)/ir_Carrier.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Carrier.cpp

ir_Haier.o : $(USER_DIR)/ir_Haier.cpp $(USER_DIR)/ir_Haier.h $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Haier.cpp

ir_Hitachi.o : $(USER_DIR)/ir_Hitachi.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Hitachi.cpp

ir_GICable.o : $(USER_DIR)/ir_GICable.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_GICable.cpp

ir_Whirlpool.o : $(USER_DIR)/ir_Whirlpool.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Whirlpool.cpp

ir_Lutron.o : $(USER_DIR)/ir_Lutron.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Lutron.cpp

ir_Electra.o : $(USER_DIR)/ir_Electra.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Electra.cpp

ir_Pioneer.o : $(USER_DIR)/ir_Pioneer.cpp $(GTEST_HEADERS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_Pioneer.cpp

ir_MWM.o : $(USER_DIR)/ir_MWM.cpp $(USER_DIR)/ir_RC5_RC6.cpp $(COMMON_DEPS)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $(USER_DIR)/ir_MWM.cpp
