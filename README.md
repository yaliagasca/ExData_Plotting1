> View(household_power_consumption)
> t <- read.table("household_power_consumption.txt", header=TRUE, sep=";", na.strings = "?", colClasses = c('character','character','numeric','numeric','numeric','numeric','numeric','numeric','numeric'))
> t$Date <- as.Date(t$Date, "%d/%m/%Y")
> t <- subset(t,Date >= as.Date("2007-2-1") & Date <= as.Date("2007-2-2"))
> t <- t[complete.cases(t),]
> dateTime <- paste(t$Date, t$Time)
> dateTime <- setNames(dateTime, "DateTime")
> t <- t[ ,!(names(t) %in% c("Date","Time"))]
> t <- cbind(dateTime, t)
> t$dateTime <- as.POSIXct(dateTime)
> hist(t$Global_active_power, main="Global Active Power", xlab = "Global Active Power (kilowatts)", col="red")
> dev.copy(png,"plot1.png", width=480, height=480)
png 
  4 
> dev.off()
RStudioGD 
        2 
> plot(t$Global_active_power~t$dateTime, type="l", ylab="Global Active Power (kilowatts)", xlab="")
> dev.copy(png,"plot2.png", width=480, height=480)
png 
  4 
> dev.off()
RStudioGD 
        2 
> with(t, {
+     plot(Sub_metering_1~dateTime, type="l",
+          ylab="Global Active Power (kilowatts)", xlab="")
+     lines(Sub_metering_2~dateTime,col='Red')
+     lines(Sub_metering_3~dateTime,col='Blue')
+ })
> legend("topright", col=c("black", "red", "blue"), lwd=c(1,1,1), 
+        c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"))
> dev.copy(png, file="plot3.png", height=480, width=480)
png 
  4 
> dev.off()
RStudioGD 
        2 
> par(mfrow=c(2,2), mar=c(4,4,2,1), oma=c(0,0,2,0))
> with(t, {
+     plot(Global_active_power~dateTime, type="l", 
+          ylab="Global Active Power (kilowatts)", xlab="")
+     plot(Voltage~dateTime, type="l", 
+          ylab="Voltage (volt)", xlab="")
+     plot(Sub_metering_1~dateTime, type="l", 
+          ylab="Global Active Power (kilowatts)", xlab="")
+     lines(Sub_metering_2~dateTime,col='Red')
+     lines(Sub_metering_3~dateTime,col='Blue')
+     legend("topright", col=c("black", "red", "blue"), lty=1, lwd=2, bty="n",
+            legend=c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"))
+     plot(Global_reactive_power~dateTime, type="l", 
+          ylab="Global Rective Power (kilowatts)",xlab="")
+ })
> dev.copy(png, file="plot4.png", height=480, width=480)
png 
  4 
> dev.off()
RStudioGD 
        2 
