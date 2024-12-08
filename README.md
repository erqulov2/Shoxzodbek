package main

import "fmt"

	type Car struct {
		ID int
		Brand string
		Rented bool
	}
	type Bike struct {
		ID int
		Brand string
		Rented bool
	}
	type Skate struct {
		ID int
		Brand string
		Rented bool
	}

	type Vehicle interface {
		Rent() error 
		Return() error
		Details()
	}

	func (c *Car) Rent() error {
		if c.Rented {
			return errors.New("Bu moshina ijaraga olingan")
		}
		c.Rented = true
		return nil
	}
    
	func (c *Car) Return()  error {
		if !c.Rented{
			return errors.New("Bu moshina ijaraga olinmagan")
		}
		c.Rented = false
		return nil
	}

	func (c *Car) Details(){
		fmt.Println("Car-ID:%d,Brand%s,Rented:%t\n",c.ID,c.Brand,c.Rented)
	}
    

	func (b *Bike) Rent() error {
		if b.Rented {
			return errors.New("Bu velosiped ijaraga olingan")
		}
		b.Rented = true
		return nil
	}
	func (b *Bike) Return() erroor {
		if !b.Rented{
			return errors.New("Bu velosiped ijaraga olinmagan")
		}
		b.Rented = false
		return nil
	}
	func (b *Bike) Details(){
		fmt.Println("Bike-ID:%d,Brand:%s,Rented:%t\n",b.ID,b,Brand,b.Rented)
	}


	func (s *Skate) Rent() error {
		if s.Rented {
			return errors.New("Bu skeyt ijaraga olingan")
		}
		s.Rented = true
		return nil
	}  
	func (s *Skate) Rented() error {
		if !s.Rented{
			return errors.New("Bu skeyt ijaraga olinagan")
		}
		s.Rented = false
		return nil
	}
	 func (s *Skate) Details(){
		fmt.Println("Skate-ID:%,Brand:%s,Rented:%t\n",s.ID,s.Brand,s.Rented)
	 }

	 func main(){
		var vehicles []Vehicle
		var choice int

		for{
			fmt.Println("1.Add Vehicle")
			fmt.Println("2.Rent Vehicle")
			fmt.Println("3.Return Vehicle")
			fmt.Println("4.Show Details")
			fmt.Println("5.Exit")
			fmt.Print("Variantni tanlang:")
			fmt.Scanln(&tanlash)

		    switch tanlash{
			case 1:
            fmt.Println("Avto turini kiriting (car/bike/skate):")
			var vType string
			fmt.Scanln(&vType)
			fmt.Println("ID va Brand kiriting:")
			var id int
			var brand string
			fmt.Scanln(&id, &brand)
			vType = strings.ToLower(vType)

			switch vType{
			case "car":
				vehicles = append(vehicles, &Car{ID: id, Brand: brand})
			case "bike":
				vehicles = append(vehicles, &Bike{ID: id, Brand: brand}) 
			case "skate":
				vehicles = append(vehicles, &Skate{ID: id, Brand: brand})
			default:
				fmt.Println("Yaroqsiz avto turi")
			}
		case 2:
			fmt.Println("Ijaraga olinadigan avto ID sini kiriting")
			var id int
			fmt.Scanln(&id)
			found := false
			for _, v := range vehicles {
				switch v := v.(turi){
				case *Car, *Bike, *Skate:
					if id == v.(*Car).ID {
						err := v.Rent()
						if err != nil {
							fmt.Println(err)
						} else {
							fmt.Println("Avto muvaffaqiyatli ijaraga olingan")
						}
						found = true
						break
					}
				}
			}
			if !found {
				fmt.Println("Avto topilmadi")
			}
		case 3:
			fmt.Println("Qaytarish uchun avto ID sini kiriting:")
			var id int
			fmt.Scanln(&id)
			found := false
			for _, v := range vehicles {
				switch v := v.(turi) {
				case *Car, *Bike, *Skate:
					if id == v(*Car).ID {
						err := v.Return()
						if err != nil {
							fmt.Println(err)
						} else {
							fmt.Println("Avto muvaffaqiyatli o'zgartirilgan")
						}
						found = true
						break
					}
				}
			}
			if !found {
				fmt.Println("Avto topilmadi")
			}
		case 4:
			for _, v := range vehicles {
				v.Details()
			}
		case 5:
			return

		default:
			fmt.Println("Xato tanlov")
			}
		}
	 }
