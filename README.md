# socket.io-angular-chat

# sending message to server

sendMessage() {
    this.socket.emit('chat', {message: this.message, user: this.user, room: this.room});
  }

# received message through observable
  receiveMessage() {
    this.getMessage().subscribe((data) => {
      this.incomingMessage.push(data);
    });
  }

 # get message from server
 getMessage() {
    return new Observable<any>(observer => {
      this.socket.on('chat', (data: any) => observer.next(data));
    });
  }
