les classes
-----------

l'équivalent d'une classe php en go est une **structure**

    // Human.php
	class Human
	{
		/** @var string */
		public $gender

		/** @var string */
		private $nickname
	}

Go

	# human.go
	type Human stuct {
    	Gender   string
	    nickname string
	}

Notez qu'il n'existe pas de mot clé définissant la visibilité des variables en go,en php nous disposons de 3 types : **public**, **protected**, **private**, avec go, il n'y a que 2 types disponibles, pour lesquels il n'existe pas de mot clé, la règle étant la suivante

	type Human stuct {
    	Gender   string // public car le nom de la propriété commence par une majuscule
	    nickname string // private|protected car le nom de la propriété commence par une minuscule
	} 
	
go ne s'encombre pas de mots clés, la case de la première lettre d'une propriété suffit a en définir la visibilité.

les méthodes
------------
Il n'existe pas à proprement parler de **méthodes** en go, au lieu d'attacher une classe à une fonction, nous définissons la structure sur laquelle la fonction sera disponible.

	<?php
	// Human.php
	
	class Human
	{
		/** @var string */
		public $gender

		/** @var string */
		private $nickname
		
		/**
		 * @return string
		 */
		public function getGenderNickname()
		{
			return $this->gender . ' ' . $this->nickname;
		}
	}

Go
	
	# human.go
	type Human stuct {
    	Gender   string
	    nickname string
	}
	
	func (h *Human) GetGenderNickname() string {
		return h.Gender + " " + h.nickname
	}

En php, le fait que la function soit encapsulée dans la classe Human en fait une méthode de cette même classe, tandis qu'en go c'est la première partie de la définition de la fonction qui en fait une méthode de la structure *Human*, **func (h *Human)**, et là encore, la visibilité de la méthode est gérée par la case de la première lettre de la fonction.


les interfaces
--------------
En php, on déclare une **interface** de la manière suivante

	<?php
	// Human.php
	
	interface Walker
	{
		public function walk();
	} 
	
	class Human implement Walker
	{
		/** @var string */
		public $gender

		/** @var string */
		private $nickname
		
		/**
		 * @return string
		 */
		public function getGenderNickname()
		{
			return $this->gender . ' ' . $this->nickname;
		}
		
		public function walk()
		{
			echo "walking…\n";
		}
	}

en Go

	# human.go
	type Human stuct {
    	Gender   string
	    nickname string
	}
	
	type Walker interface {
    	Walk()
	}
	
	func (h *Human) GetGenderNickname() string {
		return h.Gender + " " + h.nickname
	}
	
	func (h *Human) Walk() {
		fmt.Println("walking…")
	}
	
Le simple fait que la **struct** Human dispose d'une méthode Walk() fait qu'implicitement elle implémente l'interface Walker, tandis qu'avec php nous précison là encore quelle(s) interface(s) la classe étend avec le mot clé `implements`.