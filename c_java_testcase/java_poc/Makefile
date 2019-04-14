# next generation Makefile

CASE_SRC = src
RULE_SRC = rule
CASE_OBJ = case_obj
RULE_OBJ = rule_obj
OUTPUT   = output/jarfiles

PKG_NAME = poc/mx_poc
RULE_PKG = io/xc5

CASE.JAR = case.jar
RULE.JAR = rule.jar

TARGET = $(CASE.JAR) $(RULE.JAR)

JAR    = jar
JAVAC  = javac

VPATH = $(CASE_SRC)/$(PKG_NAME)

.PHONY: all compile_case compile_rule clean test_scan

all: $(TARGET)
	cd output; tar zcvf ../../java.tar.gz jarfiles/*.jar

scan:
	cd $(OUTPUT); \
	xvsa -xfa -c -Wf,-RBC=true $(RULE.JAR) -noinline; \
	xvsa -xfa -c $(CASE.JAR); \
	xvsa -xfa -json case.o rule.o

$(CASE.JAR): compile_case
	cd $(CASE_OBJ) && $(JAR) -cvf ../$(OUTPUT)/$@ $(PKG_NAME)/*

$(RULE.JAR): compile_rule
	cd $(RULE_OBJ) && $(JAR) -cvf ../$(OUTPUT)/$@ $(PKG_NAME)/* 

compile_case:
	@-mkdir -p $(CASE_OBJ)
	@-mkdir -p $(OUTPUT)
	$(JAVAC) -g -sourcepath $(CASE_SRC) -d $(CASE_OBJ) $(CASE_SRC)/$(PKG_NAME)/*.java

compile_rule:
	@-mkdir -p $(OUTPUT)
	@-mkdir -p $(RULE_OBJ)
	$(JAVAC) -g -sourcepath $(RULE_SRC) -d $(OUTPUT) $(RULE_SRC)/$(RULE_PKG)/*.java
	$(JAVAC) -g -sourcepath $(RULE_SRC) -d $(RULE_OBJ) $(RULE_SRC)/$(PKG_NAME)/*.java

clean:
	rm -rf $(TARGET) $(CASE_OBJ)/* $(RULE_OBJ)/* $(OUTPUT)/*
