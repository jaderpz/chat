# chat
<!DOCTYPE html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<title>Urabacile</title>
	<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
    <link href='https://fonts.googleapis.com/css?family=Montserrat:400,700' rel='stylesheet' type='text/css'>
    <link href="https://fonts.googleapis.com/css?family=Acme" rel="stylesheet"> 
	<link rel="stylesheet" href="css/bootstrap.min.css">
	<link rel="stylesheet" href="css/estilo.css">
</head>
<body>
	<header id="header" class="header navbar-fixed-top">  
    
        <div class="container ">   
            <nav class="main-nav" role="navigation">
                <div class="navbar-header text-center">
                    <button class="navbar-toggle" type="button" data-toggle="collapse" data-target="#navbar-collapse">
                            <span class="icon-bar-wrapper">
                        	 
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </span>
                    </button>
                    <a class="navbar-brand" href="#"><img src="images/logo.png" alt=""></a>
                   <div class="navbar-brand">
                   <a href="#"><i class="fa fa-play-circle"></i></a>
                   <a href="#"><i class="fa fa-power-off"></i></a>
                    </div>
                </div>
                <div id="navbar-collapse" class="navbar-collapse collapse  text-center">
                    <ul class="nav navbar-nav center-block">
                        <li class="nav-item"><a class="scrollto" href="#"><i class="fa fa-comments"></i> Chat</a></li>
                        <li class="nav-item"><a class="scrollto" href="#"><i class="fa fa-trophy"></i> Juegos</a></li>
                        <li class="nav-item"><a class="scrollto" href="#"><i class="fa fa-book"></i> Aprender</a></li>
 						<li class="nav-item"><a class="scrollto" href="#"><i class="fa fa-user"></i> Usuario</a></li>                        <li class="nav-item"><a class="scrollto" href="#"><i class="fa fa-heart"></i> Contacto</a></li>
                        <li class="nav-item"><a href="#" data-toggle="modal" data-target="#rsvp-modal"><i class="fa fa-sign-out" aria-hidden="true"></i>
 Salir</a></li>
                    </ul>
                </div>
            </nav>
        </div>
    </header>
	<div class="container">
		<section class="main row">
			<article class="col-xs-12 col-sm-8 col-md-9 text-center">
				
				<div  class="container-fluid">
			<section  style="padding: 10%; padding-top:2%">			
				<div class="row">				
					<h2>Sala de Chat: <small>Racha</small></h2>	
				</div>	
				<div class="row">
					<form id="formChat" role="form">
						<div class="form-group">
                            <label id "eMensaje" for="eMensaje"></label>
							<label for="usuario">Usuario</label>
							<input type="text" class="form-control" id="user" name="user" onkeyup="comprovarCampo(this.value)" placeholder="Digite Usuario">
						</div>
						<div class="form-group">							
							<div class="row">
								<div class="col-md-12" >
									<div id="conversation" style="height:250px; border: 1px solid #CCCCCC; padding: 10px;  border-radius: 5px; overflow-x: hidden;">
										
									</div>
								</div>
							</div>
						</div>
						<div class="form-group">				
							<label for="message">Mensaje</label>
							<textarea id="message" name="message" onkeyup="nombreBoton(this.value)" placeholder="Escribir Mensaje"  class="form-control" rows="3" required></textarea>
						</div>
					  <button id="send" class="btn btn-primary" disabled>Primero escribe</button>
					</form>
				</div>
			</section>	
		</div>	
		<script src="http://ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>		
		<script src="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
		<script>
		
			$(document).on("ready", function(){	
				registerMessages();
				$.ajaxSetup({"cache": false});
				setInterval("load01dMessages()", 500);
				

			});

			var comprovarCampo = function(user)	{
				if ($("#user").text() == ""){
					send.disabled = true;
				}
				if ($("#user").text() != ""){
					send.disabled = false;
				}
			}	

			function nombreBoton(message){
				$.ajax()
				if ($("#message").val() === ""){
					var nBoton = " Ahh, eso era bueno";
					$("#send").text(nBoton);
					send.disabled = true;
				}
				if ($("#message").val() != ""){
					var nBoton = " Enviar";
					$("#send").text(nBoton);
					send.disabled = false;
				}
				if ($("#message").val() == "mierda"){
					var nBoton = " Sin Groserias pues";
					$("#send").text(nBoton);
					send.disabled = true;
				}
				if ($("#message").val() == "mierda"){
					var nBoton = " Sin Groserias pues";
					$("#send").text(nBoton);
					send.disabled = true;
				}
			}

			var registerMessages = function(){
				$("#send").on("click", function(e){
					e.preventDefault();
					var frm = $("#formChat").serialize();
					if ($("#user").val()!=""){
					$.ajax({
						type: "POST",
						url: "register.php",
						data: frm
					}).done(function(info){
						$("#message").val(""); //<-- Limpia
						send.disabled = true;
						// <-- var altura = $("#conversation").prop("scrollHeight"); $("#conversation").scrollTop(altura);
						console.log ( info );
					});//<punto y coma
				
					}else{
						var tex ="Falta Usuario";
						$("#eMensaje").text(tex);
					}
			}); 
			}

			var load01dMessages = function(){
				$.ajax({
					type: "POST",
					url: "conversation.php"
				}).done(function(info){
					$("#conversation").html( info );
					$("#conversation p:last-child").css({"background-color": "lightgreen",
														"padding-botton": "20px"});
					var altura = $("#conversation").prop("scrollHeight");
					$("#conversation").scrollTop(altura);
				});
			}
			
		</script>
</article>
		  <aside class="col-xs-12 col-sm-4 col-md-3">
			<h3>Publicidad</h3>
			  <p>Contrata ya tu internet, con directv. Lideres en entretenimiento. Para comprar dale <a href="#">click aqui </a> tenemos todo lo que siempre has querido </p>
				<p> Directv te cambia la visa</p>
			</aside>
		</section>
		<div class="row">
			<article class="color1 col-xs-12 col-sm-6 col-md-3">
			  <h3>titulo</h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Magnam obcaecati quam adipisci vero accusantium nesciunt sed. Consectetur ducimus sapiente, dolorem vel expedita deleniti cumque, quaerat sit quo fugit, omnis laborum.</p>
              
</article>
			<article class="col-xs-12 col-sm-6 col-md-3">
				<h3>Radio</h3>
				<p>En la radio puedes programar la musica que mas te guste. Solo debes pedir canciones en el chat. Recuarda que el chat general es muy restringido si quieres mayor liberta puedes ir a <a>otras salas de chat</a></p>
			</article>
			<article class ="clearfix visible-sm-block"></article>
			<article class="color1 col-xs-12 col-sm-6 col-md-3">
				<h3>Columna</h3>
				<p>programa de aprendizaje.</p>
                <p>programa de aprendizaje.</p>
                <p>programa de aprendizaje.</p>
                <p>programa de aprendizaje.</p>
                <p>programa de aprendizaje.</p>
			</article>
			<article class="col-xs-12 col-sm-6 col-md-3">
				<h3>Preguntas frecuentes</h3>
				<ul>
                <li> Como quito la radio</li>
                <li> Como adtualizo mi perfil</li>
                <li> Como cambio mi foto</li>
                <li> Donde redimir los puntos</li>
                <li> Puedo administrar un chat?</li>
                <li> Para que es el nivel <a href="#"> Mas preguntas</a></li>
                </ul>
			</article>
		</div>
	</div>

	<footer>
    <div class="sombra">
    </div>
	 	<div class="container">
            <div class="row">
                <div class="col-md-12 text-center   wow fadeInUp animated">
                    <div class="social">
                        <h2>Redes Sociales</h2>
                        <ul class="icon_list">
                            <li><a href="http://www.facebook.com/jajader"target="_blank"><i class="fa fa-facebook"></i></a></li>
                            <li><a href="http://www.twitter.com/jajader"target="_blank"><i class="fa fa-twitter"></i></a></li>
                            <li><a href=""><i class="fa fa-google-plus"></i></a></li>
                            <li><a href=""><i class="fa fa-linkedin"></i></a></li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        
        
	    <div class="derechos col-md-12 text-center">
	      <h4>Jhon Jader</h4>
	      <p>© 2017 | Todos los derechos reservados.</p>
        </div>
	  
	</footer>
	<!-- <script src="js/jquery.js"></script> -->
	<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script> 
	<script src="js/bootstrap.min.js"></script>
</body>
</html>
