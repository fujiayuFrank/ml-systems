
# Makefile for ML Systems Midterm Exam
# Generates both student version (no solutions) and solution version

.PHONY: all clean distclean exam solution

# Default target: build both versions
all: exam solution

# Student version (no solutions)
exam: exam.pdf

exam.pdf: exam.tex instructions.tex questions.tex feamster.sty
	@echo "Building student version (no solutions)..."
	pdflatex -synctex=1 -interaction=nonstopmode -halt-on-error exam.tex
	pdflatex -synctex=1 -interaction=nonstopmode -halt-on-error exam.tex
	@echo "Student version created: exam.pdf"

# Solution version (with solutions)
solution: exam-solution.pdf

exam-solution.pdf: exam.tex instructions.tex questions.tex feamster.sty
	@echo "Building solution version..."
	python -c "from pathlib import Path; p=Path('exam.tex'); s=p.read_text(encoding='utf-8'); old=r'\usepackage[]{feamster}'; assert old in s, 'Package declaration not found'; s=s.replace(old, r'\usepackage[solution]{feamster}'); Path('exam-solution.tex').write_text(s, encoding='utf-8')"
	pdflatex -synctex=1 -interaction=nonstopmode -halt-on-error exam-solution.tex
	pdflatex -synctex=1 -interaction=nonstopmode -halt-on-error exam-solution.tex
	@echo "Solution version created: exam-solution.pdf"

# Clean up auxiliary files and PDFs
clean:
	python -c "from pathlib import Path; extensions={'.aux','.log','.out','.toc','.lof','.lot','.fls','.fdb_latexmk','.synctex.gz'}; [p.unlink() for p in Path('.').iterdir() if p.is_file() and (any(p.name.endswith(e) for e in extensions) or p.name in {'exam-solution.tex','exam.pdf','exam-solution.pdf'})]"

# Clean everything including PDFs
distclean: clean
