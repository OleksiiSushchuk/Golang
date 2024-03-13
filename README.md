package main

import "fmt"

type Situation struct {
	Discription string
	Choise      []string
	Next        []Situation
}

func main() {
	startSituation := Situation{
		Discription: "Назар прокидається на пустелій дорозі в середині невідомого лісу ",
		Choise:      []string{"Пройти дорогою вперед", "Повернути назад і шукати сліди, які привели його сюди."},
		Next:        []Situation{},
	}
	startSituation.Next = append(startSituation.Next, Situation{
		Discription: "Назар продовжує свій шлях через пустелю дорогою, яка веде до замку.Після кількох годин ходьби він доходить до старої руїни замку, де знаходить залишки давньої цивілізації. Тут він знаходить карту, яка вказує на схованку, де може бути ключ до його минулого. Однак, під час пошуку він натрапляє на пастку та опиняється в підземному лабіринті.",
		Choise:      []string{"Досліджувати руїни замку", "Шукати виходу з лабіринту"},
		Next:        []Situation{},
	})
	startSituation.Next = append(startSituation.Next, Situation{
		Discription: "Назар розпочинає ретельний обмірок місця, де він прокинувся. Він виявляє сліди, які ведуть до невеликої стоянки віддаленого поштового відділення. Тут він знаходить записку, яка розповідає про те, що він був учасником аварії літака і потрапив у ліс.",
		Choise:      []string{"Дослідити стоянку, можливо тут знайдуться корисні речі.", "Шукати інший шлях до цивілізації, обходячи ліс"},
		Next:        []Situation{},
	})
	startSituation.Next[0].Next = append(startSituation.Next[0].Next, Situation{
		Discription: "Назар знаходить ключ до однєї з кімнат замку",
		Choise:      []string{"Відкрити кімнату", "Краще не відкривати, може бути небезечно"},
		Next:        []Situation{},
	})
	startSituation.Next[0].Next = append(startSituation.Next[0].Next, Situation{
		Discription: "Назар вдається до розумних виходів та відкриває собі шлях назовні, де зустрічає рятувальну команду",
		Choise:      []string{},
		Next:        []Situation{},
	})
	startSituation.Next[0].Next[0].Next = append(startSituation.Next[0].Next[0].Next, Situation{
		Discription: "В кімнаті знайшов карту виходу та врятувався",
		Choise:      []string{},
		Next:        []Situation{},
	})
	startSituation.Next[0].Next[0].Next = append(startSituation.Next[0].Next[0].Next, Situation{
		Discription: "Назар не зміг врятуватися",
		Choise:      []string{},
		Next:        []Situation{},
	})
	startSituation.Next[1].Next = append(startSituation.Next[1].Next, Situation{
		Discription: "Назар так і не знайшов підсказок що робити",
		Choise:      []string{},
		Next:        []Situation{},
	})
	startSituation.Next[1].Next = append(startSituation.Next[1].Next, Situation{
		Discription: "Назар знаходиться портал, що відкриває йому доступ до втрачених спогадів та відновлення пам'яті",
		Choise:      []string{},
		Next:        []Situation{},
	})
	play(startSituation)
}

func play(activeSituation Situation) {
	fmt.Println(activeSituation.Discription)
	if len(activeSituation.Choise) == 0 {
		fmt.Println("Гра завершена")
		return
	}
	fmt.Println("Оберіть варіант")
	for i, choise := range activeSituation.Choise {
		fmt.Println(i+1, choise)
	}
	var number int
	fmt.Println("Ваш варіант:")
	_, err := fmt.Scan(&number)
	if err != nil || number < 1 || number > len(activeSituation.Choise) {
		fmt.Println("Невірний варіант, спробуйте ще раз")
		fmt.Scanln()
		play(activeSituation)
		return
	}
	nextIndex := number - 1
	if nextIndex >= 0 && nextIndex < len(activeSituation.Next) {
		nextSituation := activeSituation.Next[nextIndex]
		fmt.Println()
		play(nextSituation)
	} else {
		fmt.Println("Невірний варіант, спробуйте ще раз")
		fmt.Scanln()
		play(activeSituation)
	}
}
