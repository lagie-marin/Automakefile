SRC = calc.c \
	src/main.c \

HEADERS_DIR = -Iinclude \
	-Iinclude/calc/calc.h \
	-Iinclude/fakeProj.h \

CC = gcc
SOURCES_DIR = .
CFLAGS += -ftest-coverage -O2
LIBS = -lm \

BCK_DIR = backup
ZIP = tar
ZIPFLAGS = -cvvf
UNZIP = tar
UNZIPFLAGS = -xvf
OBJ = $(SRC:.c=.o)
V = 4.45

all: $(OBJ) $(SOURCES_DIR)
	${CC} $(OBJ) $(HEADERS_DIR) $(LIBS)

clean:
	rm -f $(SOURCES_DIR)/$(OBJ)
	rm -f $(SOURCES_DIR)/vgcore.*
	rm -f $(SOURCES_DIR)/*.gcno

fclean: clean
	rm -f $(SOURCES_DIR)/a.out
re: fclean all

num:
	@echo $$(($$(cat .version)))


archive:
	mkdir -p $(BCK_DIR)
	$(ZIP) $(ZIPFLAGS) $(BCK_DIR)/a.out_$(V).$(ZIP) $(SRC);
	echo $$(($$(cat .version) + 1)) > .version
	echo "a.out_$(V).$(ZIP) file generated.";

revert:
	@VERSION=$$(($$(cat .version) - 1)); \
	if [ $$VERSION -lt 0 ]; then \
		VERSION=0; \
	fi; \
	if [ -f $(BCK_DIR)/$(EXEC)_$(V).$(ZIP) ]; then \
		$(UNZIP) $(UNZIPFLAGS) $(BCK_DIR)/$(EXEC)_$(V).$(ZIP); \
	else\
		echo "Backup file $(BCK_DIR)/$(EXEC)_$(V).$(ZIP) does not exist."; \
	fi; \
	if [ $$(cat .version) -gt 0 ]; then \
		echo $$(($$(cat .version) - 1)) > .version; \
	fi

delete:
	@if [ -f $(BCK_DIR)/a.out_$(V).$(ZIP) ]; then \
		rm $(BCK_DIR)/a.out_$(V).$(ZIP); \
	else \
		echo "Backup file $(BCK_DIR)/a.out_$(V).$(ZIP) does not exist."; \
	fi

