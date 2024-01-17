# Angular 17 Hijri Date Picker using Angular Material Example

This project is a template of how to use angular material for hijri calendar system.

## For Knowledge only

You have to install those libraries

```
npm install ngx-angular-material-hijri-adapter

ng add @angular/material

npm install moment-hijri
```

## Import Libraries & Providers

If your project standalone you will import the libraries and providers in the component inself such as:

```
import { Component, Inject, OnInit } from '@angular/core';
import { MatButtonModule } from '@angular/material/button';
import { MatMomentDateModule } from '@angular/material-moment-adapter';
import {
  MatDatepickerModule,
  MatDatepickerIntl,
} from '@angular/material/datepicker';
import { MatInputModule } from '@angular/material/input';
import { MatFormFieldModule } from '@angular/material/form-field';
import {
  DateAdapter,
  MAT_DATE_FORMATS,
  MAT_DATE_LOCALE,
} from '@angular/material/core';
import 'moment/locale/ar-sa';
import { NgxAngularMaterialHijriAdapterModule } from 'ngx-angular-material-hijri-adapter';
import {
  NgxAngularMaterialHijriAdapterService,
  DateLocaleKeys,
  MOMENT_HIJRI_DATE_FORMATS,
} from 'ngx-angular-material-hijri-adapter';

@Component({
  selector: 'app-root',
  providers: [
    {
      provide: DateAdapter,
      useClass: NgxAngularMaterialHijriAdapterService,
    },
    // Change the format by using `MOMENT_HIJRI_DATE_FORMATS` for Dates and `MOMENT_HIJRI_DATE_TIME_FORMATS` for date/time.
    { provide: MAT_DATE_FORMATS, useValue: MOMENT_HIJRI_DATE_FORMATS },
    // Change the localization to arabic by using `AR_SA` not `AR` only and `EN_US` not `EN` only.
    { provide: MAT_DATE_LOCALE, useValue: DateLocaleKeys.AR_SA },
  ],
  standalone: true,
  imports: [
    MatFormFieldModule,
    MatInputModule,
    MatDatepickerModule,
    MatButtonModule,
    NgxAngularMaterialHijriAdapterModule,
    MatMomentDateModule,
  ],

  templateUrl: './app.component.html',
  styleUrl: './app.component.scss',
})

```

## Class Code

```
export class AppComponent implements OnInit {
  title = 'Angular Hijri Date Picker using Angular Material Example';
  constructor(
    private _adapter: DateAdapter<any>,
    private _intl: MatDatepickerIntl,
    @Inject(MAT_DATE_LOCALE) private _locale: string
  ) {}

  ngOnInit() {
    let lang = 'ar-sa';
    this._adapter?.setLocale(lang);
  }

  french() {
    this._locale = 'ar-sa';
    this._adapter.setLocale(this._locale);
  }

  updateCloseButtonLabel(label: string) {
    this._intl.closeCalendarLabel = label;
    this._intl.changes.next();
  }

  getDateFormatString(): string {
    if (this._locale === 'ja-JP') {
      return 'YYYY/MM/DD';
    } else if (this._locale === 'fr') {
      return 'DD/MM/YYYY';
    }
    return '';
  }
}
```

## Thankfulness

I would thanks to developer [Ebrahiem-Gamal-Mohamed](https://github.com/Ebrahiem-Gamal-Mohamed) for creating such a greatful Hijri Date Adapter.
