define check_build_folder
	@if [ ! -d $(1) ]; then mkdir -p $(1); fi
endef

full:
	@$(call check_build_folder, build)
	@echo "Full build"
	pdflatex -synctex=1 -jobname="full" full.tex
	rm -f *.aux *.log *.out *.synctex.gz
	mv full.pdf build/
	@echo "Full build done"

all: full module-all tugas-all

build-module:
	@$(call check_build_folder, build)
	@echo "Build Partial Module"
	@if [ -z "$(module)" ]; then \
		echo "Error: Module are not set"; \
		echo "Usage: make module module=3"; \
		exit 1; \
	fi
	@if [ ! -f "materi/pertemuan$(module).tex" ]; then \
		echo "Error: Materi for module $(module) does not exist"; \
		exit 1; \
	fi
	pdflatex -synctex=1 -jobname="pertemuan$(module)" "\def\modulenumber{$(module)} \input{module.tex}"
	rm -f *.aux *.log *.out *.synctex.gz
	mv "pertemuan$(module).pdf" build/


module-all:
	@$(call check_build_folder, build)
	@echo "Build All Partial Module"
	@count=0; \
	for file in materi/*.tex; do \
		if [ -f "$$file" ]; then \
			count=$$((count + 1)); \
			echo "Building module $$count"; \
			pdflatex -synctex=1 -jobname="pertemuan$$count" "\def\modulenumber{$$count} \input{module.tex}" ; \
		fi \
	done
	rm -f *.aux *.log *.out *.synctex.gz
	mv "pertemuan"*.pdf build/

new-module:
	@echo "Create new materi"
	@if [ -z "$(module)" ]; then \
		echo "Error: Module are not set"; \
		echo "Usage: make new-materi module=3"; \
		exit 1; \
	fi
	@if [ -f "materi/pertemuan$(module).tex" ]; then \
		echo "Error: Materi for module $(module) already exist"; \
		exit 1; \
	fi
	@echo "Create new materi for module $(module)"
	@echo "\begin{center}" >> materi/pertemuan$(module).tex
	@echo -e "\\\textbf{Modul $(module) Praktikum [MATA KULIAH PRAKTIKUM]}\n" >> materi/pertemuan$(module).tex
	@echo "\textbf{JUDUL MATERI}" >> materi/pertemuan$(module).tex
	@echo "\end{center}" >> materi/pertemuan$(module).tex	

build-tugas:
	@echo "Build Tugas"
	pdflatex -synctex=1 -jobname="tugas$(tugas)" "\def\tugasnumber{$(tugas)} \input{tugas.tex}"
	rm -f *.aux *.log *.out *.synctex.gz
	mv "tugas$(tugas).pdf" build/

tugas-all:
	@echo "Build All Tugas"
	@count=0; \
	for file in tugas/*.tex; do \
		if [ -f "$$file" ]; then \
			count=$$((count + 1)); \
			echo "Building tugas $$count"; \
			pdflatex -synctex=1 -jobname="tugas$$count" "\def\tugasnumber{$$count} \input{tugas.tex}" ; \
		fi \
	done
	rm -f *.aux *.log *.out *.synctex.gz
	mv "tugas"*.pdf build/

new-tugas:
	@echo "Create new tugas"
	@if [ -z "$(tugas)" ]; then \
		echo "Error: Tugas are not set"; \
		echo "Usage: make new-tugas tugas=3"; \
		exit 1; \
	fi
	@if [ -f "tugas/tugas$(tugas).tex" ]; then \
		echo "Error: Tugas for tugas $(tugas) already exist"; \
		exit 1; \
	fi
	@echo "Create new tugas for tugas $(tugas)"
	@echo "\begin{center}" >> tugas/tugas$(tugas).tex
	@echo -e "\\\textbf{Tugas $(tugas)}\n" >> tugas/tugas$(tugas).tex
	@echo "\textbf{JUDUL TUGAS}" >> tugas/tugas$(tugas).tex
	@echo "\end{center}" >> tugas/tugas$(tugas).tex

clean:
	@echo "Clean build files"
	rm -rf build/*


	
