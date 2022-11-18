MomentJS is very useful and contains functionality for managing time around code. However, packages sizes and external libraries can depend upon so much more than what’s use being used and causes package sizes to dramatically increase.

The mentioned functionality can be done with raw JavaScript or typescript for better type conditioning, to save your project the space and having a more generic way of dealing with time your own way.

```
function currDayOfWeek(date?: Date): string {
  const dayNames = [
    'sunday',
    'monday',
    'tuesday',
    'wednesday',
    'thursday',
    'friday',
    'saturday',
  ];

  if (!date) {
    return dayNames[new Date().getDay()];
  } else {
    return dayNames[date.getDay()];
  }
}

function formatDate(date: Date): string {
  var ampm: string = date.getHours() >= 12 ? 'pm' : 'am';
  let paddedMonth: string = ('0' + (date.getMonth() + 1)).slice(-2);
  let minutes = date.getMinutes().toString().length == 1 ?
      '0' + date.getMinutes() :
      date.getMinutes();
  return ('0' + date.getDate()).slice(-2) + '/' + paddedMonth + '/' +
      date.getFullYear() + ' - ' + date.getHours() + ':' + minutes + ' ' +
      ampm.toUpperCase()
}

getMonthsFromRange(startDate: Date, endDate: Date) {
  return Math.abs(
      endDate.getMonth() - startDate.getMonth() +
      (12 * (endDate.getFullYear() - startDate.getFullYear())));
}

// One of the most popular used functions from MomentJS, this function is completely customisable and can be manipulated to fit your personal projects
function fromNow(endDate: Date, startDate?: Date): string {
  // if `startDate` is undefined, then use date from now  
  if (!startDate) {
    startDate = new Date();
  }
  const seconds: number =
      Math.abs(Math.floor((endDate.getTime() - startDate.getTime()) / 1000));
  let totalMonths: number;
  if (seconds < 30 * 24 * 3600) {
    totalMonths = 0;
  } else {
    totalMonths = Math.abs(getMonthsFromRange(startDate, endDate));
  }

  var future: boolean =
      (endDate.getTime() < startDate.getTime()) ? false : true;

  if (totalMonths >= 1) {
    if (totalMonths < 2) {
      return future ? 'a month' : 'a month ago';
    } else if (totalMonths >= 12) {
      if ((totalMonths / 12) == 1) {
        return future ? 'a year' : 'a year ago';
      } else {
        return Math.floor((totalMonths / 12)) +
            (future ? ' years' : ' years ago');
      }
    } else {
      return totalMonths + (future ? ' months' : ' months ago');
    }
  } else {
    var hoursDiff: number = Math.floor(
        (Math.abs(endDate.getTime() - startDate.getTime()) / 3600) / 1000);

    if (hoursDiff < 1) {
      if (seconds >= 60) {
        if (seconds == 60) {
          return future ? 'a minute' : 'a minute ago';
        } else {
          return Math.round(seconds / 60) +
              (future ? ' minutes' : ' minutes ago');
        }
      } else {
        if (seconds < 2) {
          return future ? 'a second' : 'a second ago';
        } else {
          return seconds + (future ? ' seconds' : ' seconds ago');
        }
      }
    } else if (hoursDiff >= 1 && hoursDiff < 24) {
      if (hoursDiff < 2) {
        return future ? 'an hour' : 'an hour ago';
      } else {
        return hoursDiff + (future ? ' hours' : ' hours ago');
      }
    } else {
      var days: number = Math.floor(hoursDiff / 24);
      if (days < 2) {
        return future ? 'a day' : 'a day ago';
      } else {
        return days + (future ? ' days' : ' days ago');
      }
    }
  }
}

function daysInMonth(month: number, year: number) {
  return new Date(year, month, 0).getDate();
}

function getDateObjectFromTimeString(
    twelveHourTimeString: string, date?: Date): Date {
  var now = !date ? new Date() : date;
  let time = twelveHourTimeString.split(':');
  now.setHours(parseInt(time[0]));
  now.setMinutes(parseInt(time[1]));
  if (time[2]) {
    now.setSeconds(parseInt(time[2]));
  } else {
    now.setSeconds(0);
  }

  return now;
}

function dateToUnixTimeStamp(date: Date): number {
  return Math.floor(date.getTime() / 1000);
}

function addSecondsToDateObject(
    manipulationValue: number, date?: Date): Date {
  if (!date) {
    date = new Date();
  }

  var unix = dateToUnixTimeStamp(date);

  return new Date((unix + manipulationValue) * 1000);
}

function unixTimestampToHoursAndMinutes(unixstamp: number) {
  var date = new Date(unixstamp * 1000);
  var minutes = '0' + date.getMinutes();

  // negative values in slice can revert the start of the string index
  return date.getHours() + ':' + minutes.slice(-2);
}

function unixTimestampToDate(unixstamp: number): Date {
  var date = new Date(0);
  date.setUTCSeconds(unixstamp);

  return date;
}
```
