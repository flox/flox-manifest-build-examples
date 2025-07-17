
UNAME_S := $(shell uname)

ifeq ($(origin FLOXBIN), undefined)
  ifeq ($(UNAME_S), Darwin)
    FLOXBIN := /usr/local/bin/flox
  else ifeq ($(UNAME_S), Linux)
    FLOXBIN := /usr/bin/flox
  else
    $(error Unsupported OS: $(UNAME_S))
  endif
endif

all:
	clang++ -O3 -std=c++17 quotes_server.cpp -o quotes-app-cpp -lboost_system -lboost_json -pthread

install:
ifndef PREFIX
	$(error PREFIX is undefined)
endif
	mkdir -p $(PREFIX)/{bin,lib,libexec}
	cp -pr quotes.json $(PREFIX)/lib
	cp -pr quotes-app-cpp $(PREFIX)/libexec
	echo "#!/usr/bin/env sh" > $(PREFIX)/bin/quotes-app-cpp$(SUFFIX)
	echo "export QUOTES_FILE=$(PREFIX)/lib/quotes.json" >> $(PREFIX)/bin/quotes-app-cpp$(SUFFIX)
	echo "exec $(PREFIX)/libexec/quotes-app-cpp" >> $(PREFIX)/bin/quotes-app-cpp$(SUFFIX)
	chmod +x $(PREFIX)/bin/quotes-app-cpp$(SUFFIX)


clean:
	rm -f quotes-app-cpp
	@$(FLOXBIN) build clean
