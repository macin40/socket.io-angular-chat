# socket.io-angular-chat

sendMessage() {
    this.socket.emit('chat', {message: this.message, user: this.user, room: this.room});

    // this.socket.on('chat', (data) => {
    //   this.message = data.message;
    //   this.user = data.user;
    // });
  }

  receiveMessage() {
    this.getMessage().subscribe((data) => {
      this.incomingMessage.push(data);
    });
  }

  ngOnInit() {
    this.socket = io('http://localhost:5000');
    this.receiveMessage();
  }

  getMessage() {
    return new Observable<any>(observer => {
      this.socket.on('chat', (data: any) => observer.next(data));
    });
  }
