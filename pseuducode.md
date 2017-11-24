simpan startScreen
simpan gameHTML
simpan selectedAnswer
simpan theClock
simpan dan tentukan counter sama dengan 30
simpan sekumpulan pertanyaan pada questionArray
simpan sekumpulan jawaban pada answerArray berdasarkan index pertanyaan
simpan sekumpulan pilihan jawaban yang benar pada correctAnswer berdasarkan index pertanyaan
simpan dan tentukan questionCounter sama dengan 0
simpan dan tentukan correctTally sama dengan 0
simpan dan tentukan incorrectTally sama dengan 0
simpan dan tentukan unansweredTally sama dengan 0

function initialScreen
	simpan button 'start quiz' pada startScreen
	tampilkan startScreen
endfunction

function generateHTML
	tentukan timer, simpan questionArray dan
		"A. +answerArray berdasarkan questionCounter index ke 0"
		"B. +answerArray berdasarkan questionCounter index ke 1"
		"C. +answerArray berdasarkan questionCounter index ke 2"
		"D. +answerArray berdasarkan questionCounter index ke 3"
	pada gameHTML
	tampilkan gameHTML
endfunction

function finalScreen
	simpan counter dan
		"All done, here's how you did!"
		"Correct Answers: +correctTally"
		"Wrong Answers: +incorrectTally"
		"Unanswered: +unansweredTally"
		button 'reset the quiz'
	pada gameHTML
	tampilkan gameHTML
endfunction

function wait
	IF questionCounter kurang dari 7:
		tambahkan 1 pada questionCounter
		panggil function generateHTML
		tentukan 30 pada counter
		panggil function timerWrapper
	ELSE
		panggil function finalScreen
	ENDIF
endfunction

function generateLossDueToTimeOut
	tambahkan 1 pada unansweredTally
	simpan counter dan 
		"You ran out of time!  The correct answer was: +correctAnswer sesuai questionCounter"
	pada gameHTML
	tampilkan gameHTML
	setTimeout 1000 pada function wait
endfunction

function generateWin
	tambahkan 1 pada unansweredTally
	simpan counter dan 
		"Correct! The answer is: +correctAnswer sesuai questionCounter"
	pada gameHTML
	tampilkan gameHTML
	setTimeout 1000 pada function wait
endfunction

function generateLoss
	tambahkan 1 pada unansweredTally
	simpan counter dan 
		"Wrong! The correct answer is: +correctAnswer sesuai questionCounter"
	pada gameHTML
	tampilkan gameHTML
	setTimeout 1000 pada function wait
endfunction

function timerWrapper
	tentukan waktu interval untuk function thirtySeconds dan simpan di theClock
	function thirtySeconds
		IF counter sama dengan 0:
			clearInterval pada theClock
			panggil function generateLossDueToTimeOut
		ENDIF
		IF counter lebih dari 0:
			counter dikurangi 1
		ENDIF
		tampilkan counter
	endfunction
endfunction

function resetGame
	tentukan questionCounter sama dengan 0
	tentukan correctTally sama dengan 0
	tentukan incorrectTally sama dengan 0
	tentukan unansweredTally sama dengan 0
	tentukan counter sama dengan 30
	panggil function generateHTML
	panggil function timerWrapper
endfunction

panggil function initialScreen
	IF onclick button 'start quiz':
		panggil generateHTML
		panggil timerWrapper
	ENDIF
		IF selectedAnswer sama dengan correctAnswer berdasarkan questionCounter:
			clearInterval pada theClock
			panggil generateWin
		ELSE
			clearInterval pada theClock
			panggil generateLoss
		ENDIF
	IF onclick 'reset the quiz':
		panggil resetGame
	ENDIF
	

















			
